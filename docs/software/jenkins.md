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
