# Installation #

Similar to the bare metal version, `docker run -i --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --restart=always jenkins/jenkins:lts` to pull the image and then start it at port 8080 on the Docker host. We then follow all the same instruction steps: install all the suggested packages and username alex.

- <https://jenkins.io/doc/book/pipeline/docker/>
- <https://hub.docker.com/r/jenkins/jenkins/>
- <https://github.com/jenkinsci/docker/blob/master/README.md>

```
node {
checkout svm
stage('Build')
{
<docker.withRegistry('http://localhost:5000')>
{
def prdImage = docker.build('nbviewer')
prdImage.push()
}
}
stage('Test')
{
<docker.withRegitstry('http://localhost:5000')>
{
docker.image('nbviewer:latest').withRun('-p 8081:8081 --name nbviewer')
{
sh 'docker ps -a'
}
}
}
}
```

We also need to install a slave node for Docker too! <https://piotrminkowski.wordpress.com/2017/03/13/jenkins-nodes-on-docker-containers/> & <https://www.docker.com/use-cases/cicd>

- <https://getintodevops.com/blog/building-your-first-docker-image-with-jenkins-2-guide-for-developers>
- <https://getintodevops.com/blog/the-simple-way-to-run-docker-in-docker-for-ci>
- <https://www.katacoda.com/courses/jenkins/build-docker-images>
- <https://devopscube.com/jenkins-master-build-slaves-docker-container/>
- <https://piotrminkowski.wordpress.com/2017/03/13/jenkins-nodes-on-docker-containers/>

Link #3 was followed by changing the mount point to not be under `/root` and use the latest Jenkins image. Also used the Jenkins JNLP slave image instead of their own solution. This gives errors on build still, but the Jenkins slave was provisioned.
