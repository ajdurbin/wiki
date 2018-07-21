# useful commands #
* stop all containers: `docker kill $(docker ps -q)`
* remove all containers: `docker rm $(docker ps -a -q)`
* remove all images: `docker rmi $(docker images -q)`

# scratch #
- <https://github.com/veggiemonk/awesome-docker>
- use traefik for reverse proxy, ssl encryption over nginx solution
- internal and external registry
- docker compose with persistent storage with scripted jobs to pull and re-deploy latest images
- kubernetes - minikube for single node host
- nvidia docker for deep learning images? not sure about these, look to be solution to installing cuda in a separate container?
- docker cloud
- docker machine, provision multiple virtual docker hosts, <https://docs.docker.com/machine/overview/>

# Resources #
- <https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes>
- <https://docs.docker.com/engine/reference/commandline/volume_rm/#usage>
- <https://docs.docker.com/docker-hub/repos/>
- <https://docs.docker.com/engine/reference/commandline/build/#tarball-contexts>
- <https://github.com/veggiemonk/awesome-docker#cicd>
