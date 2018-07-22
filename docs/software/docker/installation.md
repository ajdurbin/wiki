# Ubuntu Server Image #

Docker cannot run inside LXC containers, so we need to make a full virtual machine for it. Ubuntu server is minimal enough for this task. Start the VM with ample disk space and memory and follow installation. Skip HTTP proxy. Manual network installation if prompted, else will need to set a static IP and specify DNS there too. Select standard system utilities and OpenSSH server.

# Docker Installation

Follow <https://docs.docker.com/install/linux/docker-ce/ubuntu/>; Remove old versions
install using repository, daemon autostart, run hello-world, manage as non-root
user, start on boot, configure where docker daemon listens to connections using 
systemd version only. 

# Docker Hub #

Create an account on Docker Hub. Create a private repository "homelab".

# Docker Registry #

Selfhosted docker hub. Some issues with pulling/pushing without certificates. 
Would want to use be able to use local repository and docker hub. 

- <https://docs.docker.com/registry/deploying/#get-a-certificate>
- <https://docs.docker.com/registry/deploying/>
- <http://tech.paulcz.net/2016/01/deploying-a-secure-docker-registry/>
- <http://tech.paulcz.net/2016/01/secure-docker-with-tls/>

# Docker Compose #

Tool for defining and running multi-container Docker applications <https://docs.docker.com/compose/>.

# Docker Swarm #

For a cluster of Docker containers. Though almost everyone uses Kubernetes for this now.
