# Episode 001: Introduction and Docker Basics

- Hosted by @shashanktomar
- Recording date: TODO

## Video Checkpoints

TODO

## Agenda

- [ ] Inspiration and Introduction
  - [tgik](tgik.io)
  - lets make it a thing
- [ ] Why do you need docker and what it is?
  - build once and run anywhere (★)
  - bring actual runtime closer to developers (★★)
  - abstraction creates innovation (★★★)
- [ ] Docker vs VM
- [ ] Let's get started
  - `docker version`
  - `docker info`
  - `docker help`
- [ ] [Image vs container](./images/containers-vs-lxc-vs-vm.jpg)
- [ ] Start a container and play around with it
  - `docker run -p 80:80 nginx`
  - cleanup and `--rm`
  - detach mode `-d`
  - expose port `-p` and `-P`
  - interactive `-it`
  - environment variable `-e`
  - other Commands
    - working dir `-w` or `WORKDIR`
    - user `-u` or `USER`
    - `cp`
    - walk through `docker run --help`
    - walk through `docker --help`
  - exec
- [ ] Image Basics
  - image commands
  - buildkit
  - lets build few images
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
- [ ] Volumes
- [ ] Inspect
- [ ] Advance Topics
  - commit

## Show Notes

## Reference Links

- [tgik](tgik.io)
- [Docker docs](https://docs.docker.com/reference/)
