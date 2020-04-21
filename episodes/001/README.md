# Episode 001: Docker

- Hosted by @shashanktomar
- Recording date: TODO

## Video Checkpoints

TODO

## Agenda

- [ ] Introduction, Inspiration, Format and Audience
  - about me, about Fabric and who is this for?
  - [tgik](tgik.io)
  - the structure of the session
  - who is this for?
- [ ] Why do you need docker and what it is?

  - [Docker vs VM](./images/containers-vs-lxc-vs-vm.jpg)
  - build once and run anywhere (★)
  - bring actual runtime closer to developers (★★)
  - abstraction creates innovation (★★★)

- [ ] Image vs container
- [ ] Let's get started
  - `docker version`
  - `docker info`
  - `docker help`
- [ ] Start a container and play around with it
  - `docker run -p 80:80 nginx`
  - cleanup and `--rm`
  - detach mode `-d`
  - `attach`
  - expose port `-p` and `-P`
  - interactive `-it`
  - environment variable `-e`
  - `exec`
  - other Commands
    - working dir `-w` or `WORKDIR`
    - user `-u` or `USER`
    - `cp`
    - walk through `docker run --help`
    - walk through `docker --help`
- [ ] Health Checks
  - ```
      docker run --name=hc -d --rm \
      --health-cmd='stat /etc/passwd || exit 1' \
      --health-interval=2s \
      busybox sleep 1d
    ```
  - `watch -t "docker inspect hc | jq '.[0].State.Health.Status'"`
  - `docker exec hc rm /etc/passwd`
  - `docker exec hc touch /etc/passwd`
- [ ] Image Basics

  - let's build few images
    - noose
    - goose
  - image commands
    - walkthrough
    - `ADD` vs `COPY`
    - `ENTRYPOINT` vs `CMD`
  - buildkit
  - best practices
    - create ephemeral containers
    - understand build context
    - .dockerignore
    - multistage builds
    - keep your images thin
    - decouple applications
    - minimize the number of layers: Only the instructions RUN, COPY, ADD create layers
    - leverage build cache

### If time permits

- [ ] Storage
  - bind mounts vs volumes vs tmpfs
- [ ] Advance Topics
  - commit
  - checkpoints

## Show Notes

### Comments

### Feedback

## Reference Links

- [tgik](tgik.io)
- [Docker reference](https://docs.docker.com/reference/)
- [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Cheatsheet](./docker-cheatsheet.md)
