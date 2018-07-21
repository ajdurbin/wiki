# Installation #

Create a new container with 4GB memory and 100GB storage and follow <https://www.jfrog.com/confluence/display/RTF/Installing+on+Linux+Solaris+or+Mac+OS#InstallingonLinuxSolarisorMacOS-RPMorDebianInstallation>

```
apt install default-jre -y
echo "deb <https://jfrog.bintray.com/artifactory-debs> {distribution} {components}" | sudo tee -a /etc/apt/sources.list

Note: If you are unsure, components should be "main." To determine your distribution, run lsb_release -c

Example: echo "deb <https://jfrog.bintray.com/artifactory-debs> xenial main" | sudo tee -a /etc/apt/sources.list

curl <https://bintray.com/user/downloadSubjectPublicKey?username=jfrog> | sudo apt-key add -

sudo apt-get update
sudo apt-get install jfrog-artifactory-oss
systemctl start artifactory.service
systemctl status artifactory.service
```

Then go to <http://ip:8081/artifactory> to see the web GUI. Create an admin user and skip the rest of the steps.

# Docker Registry #

<https://www.jfrog.com/confluence/display/RTF/Docker+Registry>

Looks to be the case that this is a paid feature. There is a generic repository feature that I can look into. Alternatively we can directly use the docker server as a docker registry.


