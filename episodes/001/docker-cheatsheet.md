# Docker Cheatsheet

## Build

- CMD vs Entrypoint: The ENTRYPOINT gives a container its default nature or behavior, so that when you set an ENTRYPOINT you can run the container as if it were that binary, complete with default options, and you can pass in more options via the COMMAND

## Run

- run a container and map random ports: `docker run -P nginx`
- run a container in detached mode: `docker run -d -P nginx`
- remove on stop: `docker run --rm -P nginx`
- map ports: `docker run --rm -p=80:80 nginx`
- interactive terminal: `docker run -it --rm nginx /bin/bash`
- override working dir: `docker run -it --rm -w /var nginx /bin/bash`
- execute command as a user: `docker run -it --rm -u <user> <container> <command>`

### Health Check

- health check:
  ```
  docker run --name=hc -d --rm \
  --health-cmd='stat /etc/passwd || exit 1' \
  --health-interval=2s \
  busybox sleep 1d
  ```
- `watch -t "docker inspect hc | jq '.[0].State.Health.Status'"`
- `docker exec hc rm /etc/passwd`
- `docker exec hc touch /etc/passwd`

### Environment variables

- print existing env variables: `docker run -it --rm busybox env`
- pass a new env variable: `docker run -it -e "key=value" busybox env`
- pass a variable just by name: `export KEY=VALUE && docker run -it -e key busybox env`

### Overrides

- Four of the Dockerfile commands cannot be overridden at runtime: `FROM`, `MAINTAINER`, `RUN`, and `ADD`
- Other can be overriden, CMD, ENTRYPOINT, EXPOSE, ENV, HEALTHCHECK, VOLUME, USER, WORKDIR

## Hacks

- keep busybox running in background: `docker run -d --rm busybox sleep 1d`

## List Stuff

- list images: `docker images`
- list all images including intermediate images: `docker images -a`
- list dangling images: `docker images -f dangling=true`
- list running containers: `docker ps`
- list all containers: `docker ps -a`
- list all containers with size: `docker ps -as`
- list all exited containers: `docker ps -a -f status=exited`
- list all exited and created(a state which can result when you run a container with an invalid command) containers: `docker ps -a -f status=exited -f status=created`

## Delete Stuff

### Everything

- cleanup all dangling(not associated with a container) images, containers, volumes and networks: `docker system prune`
- additionally remove any stopped containers and all unused images (not just dangling images): `docker system prune -a`

### Images

- remove image: `docker rmi <image>`
- remove all dangling images: `docker images purge`
- remove images according to a pattern: `docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi`
- remove all images: `docker rmi $(docker images -aq)`

### Containers

- remove a container: `docker rm <id/name>`
- remove upon exit: `docker run --rm <image>`
- remove using a pattern: `docker ps -a | grep "pattern" | awk '{print $3}' | xargs docker rmi`
- remove all exited containers: `docker rm $(docker ps -a -f status=exited -q)`
- remove all exited or created(a state which can result when you run a container with an invalid command) containers: `docker rm $(docker ps -a -f status=exited -f status=created -q)`
- stop and remove all containers: `docker stop $(docker ps -q) && docker rm $(docker ps -a -q)`
- busybox incrementer: `docker run --rm busybox /bin/sh -c 'i=0; while true; do echo $i; i=$(expr $i + 1); sleep 1; done'`

### Volumes

- delete all unused volumes: `docker volume prune`
- delete a single volume: `docker volume rm <volume-name>`
- remove a container and its volume: `docker rm -v <container_name>`
