# Want #
* private, insecure registry
* multiple registries, local and docker hub

# Installation #
Without an SSL certifcate, this registry is only accessible from the Docker host. For our purposes this is okay. <https://docs.docker.com/registry/deploying/#copy-an-image-from-docker-hub-to-your-registry>

```
docker run -d \
-p 5000:5000 \
--restart=always \
--name registry \
registry:2

docker pull ubuntu:16.04
docker tag ubuntu:16.04 localhost:5000/my-ubuntu
docker push localhost:5000/my-ubuntu
docker image remove ubuntu:16.04
docker image remove localhost:5000/my-ubuntu
docker pull localhost:5000/my-ubuntu
docker container stop registry
docker container stop registry && docker container rm -v registry
curl <http://localhost:5000/v2/_catalog> # to see list of docker images
```

# links #
* <https://docs.docker.com/registry/deploying/#get-a-certificate> # deploy registry server
* <https://docs.docker.com/registry/insecure/#docker-still-complains-about-the-certificate-when-using-authentication>
* <https://www.juandebravo.com/2017/01/22/docker-insecure-registry>
* <https://coderwall.com/p/dtwc1q/insecure-and-self-signed-private-docker-registry-with-boot2docker>
*
