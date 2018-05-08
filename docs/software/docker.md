Do I want separate docker image from jenkins and git server? Still looking for good tutorial to tie together. Probably also okay if they're all on single image too. Need to find a good tutorial on this, how does docker get notified to run the image? 

Ideally would want a git push to trigger a jenkins build that pushes to artifactory (internal docker registry) that then deploys it on the docker server. All of these ideally would be separate components. 

### Ubuntu Server Image 

Docker cannot run inside LXC containers, so we need to make a full virtual machine for it. Ubuntu server is minimal enough for this task.

Start the VM with ample disk space and memory and follow installation. Skip HTTP proxy. Manual network installation. Select standard system utilities and OpenSSH server.

### Docker Installation 

https://docs.docker.com/install/linux/docker-ce/ubuntu/

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
sudo docker run hello-world
sudo systemctl enable docker
```

From 
  - http://www.littlebigextra.com/how-to-enable-remote-rest-api-on-docker-host/
  - https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd

To enable the docker API from the server, edit `/lib/systemd/system/docker.service` with `ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376` and then do `sudo systemctl daemon-reload && sudo service docker restart`. Then test the server is accessible with `curl http://dockerserverip:2376/images/json` to get a JSON string of the docker containers installed. 


### Docker Hub 

Create an account on Docker Hub. Create a private repository //homelab//.