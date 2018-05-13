### Installation 

Following documentation at `https://jenkins.io/doc/book/installing/`, create a new container with 50GB storage and 1GB memory. Follow Ubuntu instructions on the documentation

```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

Then go to `http://jenkinsip:8080` to finish the installation. Grab the Jenkins password from `/var/jenkins_home/secrets/initialAdminPassword`, choose install suggested plugins, and then create first administrator user with username alex. 

  - https://jenkins.io/doc/book/pipeline/docker/
  - https://go.cloudbees.com/docs/cloudbees-documentation/cje-user-guide/index.html#docker-workflow
  - https://getintodevops.com/blog/building-your-first-docker-image-with-jenkins-2-guide-for-developers
  - http://www.littlebigextra.com/using-jenkins-to-build-and-deploy-docker-images/
  - https://stackoverflow.com/questions/48769362/jenkins-pipeline-should-is-removing-container-on-remote-daemon-after-deployment
  - https://blog.philipphauer.de/tutorial-continuous-delivery-with-docker-jenkins/
  - https://www.digitalocean.com/community/tutorials/how-to-set-up-continuous-integration-pipelines-in-jenkins-on-ubuntu-16-04
  - https://www.thepolyglotdeveloper.com/2017/04/continuous-deployment-of-web-application-containers-with-jenkins-and-docker/
  - https://docs.docker.com/registry/deploying/#run-a-local-registry
  - https://jenkins.io/doc/book/pipeline/docker/

### Sample Jenkinsfiles 

Ideal workflow is to build on the remote docker server, push to artifactory the built image, and then pull that new image to the docker server all from jenkins. 

Something like:
```
 stage {
            steps {
                     script {
                               docker.withServer('tcp://10.10.10.10:2375') {
                               docker.withRegistry('https://registry.my.com/','jenkins-registry') {
                               docker.image('registry.my.com/image-my/my:latest').run(' -p 9090:80 -i -t --name harpal ') 

    }
                           }
                   }
            }
```

So first we would need to build the image with the server and with the registry to push it. From here we then pull the image and then rerun with server. 

From work: 

```
node {

    checkout scm

 

    stage('Build')

    {   

        docker.withRegistry('artifactory', 'credentials')

        {

            def prdImage = docker.build("project/repository")

 

            prdImage.push("latest")

        }

    }

    stage('Test / Deploy')

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            id: '/service_name/branch',

            definitionFile: 'marathon.json')

 

                def restart_uri = "/v2/apps/service_name/branch/restart"

                def reponse = httpRequest acceptType: 'APPLICATION_JSON', ignoreSslErrors: true, contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: '{"force":false}', url: "${env.MARATHON_ENDPOINT}" + restart_uri

    }

}

 

node {

    checkout scm

 

    // Define job specific variables

    def IMAGE = "project/repository"

    def REPOSITORY = "repository.example.com"

    def SERVICE_NAME = '/service/name/api'

    def BUILD_TAG = "latest"

   

    def prdImage = ""

 

    stage('Build')

    {  

        prdImage = docker.build(IMAGE)

    }

    stage('Test')

    {

        // Test cases needed

    }

    stage("Push")

    {

        docker.withRegistry('https://' + REPOSITORY, 'credentials')

        {

            prdImage.push(BUILD_TAG)

        }

    }

    stage('Deploy App')

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            id: SERVICE_NAME,

            filename: 'marathon.json',

            docker: REPOSITORY + "/" + IMAGE + ":" + BUILD_TAG,

            dockerForcePull: true)

       

        try {

            def restart_uri = "/v2/apps" + SERVICE_NAME + "/restart"

            def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, requestBody: '{"force":false}' , url: "${env.MARATHON_ENDPOINT}" + restart_uri

        }

        catch (exc) {

            echo 'Service restart failed, perhaps there was nothing to restart.'

        }

 

    }

    stage("Deploy Autoscaler")

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            filename: 'autoscaler.json',

            dockerForcePull: true)

    }

    stage("Deploy Redis")

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            filename: 'redis.json',

            dockerForcePull: true)

    }

}

 

node {

    checkout scm

 

    // Define job specific variables

    def IMAGE = "repo/service-name"

                def REPOSITORY = "artifactory.example.com"

    def BUILD_TAG = "prd_${env.BUILD_ID}"

    def SERVICE_NAME = '/service_name'

 

    stage('Build')

    {   

        docker.withRegistry('https://' + REPOSITORY, 'credentials')

        {

            def prdImage = docker.build(IMAGE)

 

            prdImage.push(BUILD_TAG)

            prdImage.push("latest")

        }

    }

    stage('Test / Deploy')

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            id: SERVICE_NAME,

            definitionFile: 'marathon.json',

            docker: REPOSITORY + "/" + IMAGE + ":" + BUILD_TAG,

            dockerForcePull: true)

    }

}

node {

    checkout scm

 

    stage('Build')

    {   

        docker.withRegistry('https://artifactory.com', 'credentials')

        {

            def prdImage = docker.build("brach/service_name")

 

            prdImage.push("latest")

        }

    }

                # will need to translate above to docker.buidlwithserver then with registry push then with registry pull and redeploy for my environment

                # dont need marathon parts

    stage('Test / Deploy')

    {

        marathon(

            url: "${env.MARATHON_ENDPOINT}",

            forceUpdate: true,

            id: '/kafka-to-cassandra/prd',

            definitionFile: 'marathon.json')

 

                def restart_uri = "/v2/apps/service_name/branch/restart"

                def reponse = httpRequest acceptType: 'APPLICATION_JSON', ignoreSslErrors: true, contentType: 'APPLICATION_JSON', httpMode: 'POST', requestBody: '{"force":false}', url: "${env.MARATHON_ENDPOINT}" + restart_uri

    }

}
```
