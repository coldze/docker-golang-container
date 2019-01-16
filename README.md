# What the hell is this? :)

This is a single container with docker and golang to build golang binaries and pack them into docker containers straight away

# Usage

* How to compile Go projects? You can refer to golang container's page: https://hub.docker.com/_/golang/
* How to build docker container? You can refer to docker's page: https://hub.docker.com/_/docker

## The purpose

The main is to combine golang and docker in one container to be able to compile golang project and build a container with it in a single run during Gitlab's CI, specifying this image as a base image for a stage in .gitlab-ci.yml.
On the other hand, it can be used anywhere.

Usage example:
you can write a script like this:
```
#!/bin/sh
mkdir build && cp ./Dockerfile ./build/Dockerfile && cd build  && go build -o my-app .. && docker build . -t my-app && docker push my-app
```
place it in your repo and execute something like:

```
docker run -P --rm -v /var/run/docker.sock:/var/run/docker.sock \
 -v $(pwd):/go/src/github.com/my-golang-test coldze/docker-golang \
 /bin/sh -c "cd /go/src/github.com/my-golang-test && ./build.sh"
```

### Docker-hub:
https://hub.docker.com/r/coldze/docker-golang
