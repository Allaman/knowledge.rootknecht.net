---
title: Docker
taxonomy:
    category:
        - DevOps
        - Docker
    author:
        - Knecht
---

[TOC]

## Prevent a container from exiting
After starting a service via docker-compose Docker will shut it down if there is no process running. To prevent that you can call a "dummy" endless command - in this case by overriding the entrypoint with a simple ping.
```yaml
entrypoint: ping localhost
```

## Show file usage of Docker on a btrfs partition
The btrfs storage driver of Docker is kind of different. A normal `df -hkl /var/lib/docker` will not show correct numers. Instead use the tools of btrfs: 
```bash
btrfs fi df /varLib/docker
```

## Docker and Proxy

### System
vim /etc/systemd/system/multi-user.target.wants/docker.service (adjust for other startup mechanism)

```
[Service]
Environment="HTTPS_PROXY=https://proxy.example.com:443/"
```

### Per build
```bash
docker build --build-arg HTTP_PROXY=proxy.company.com:3128 -t TAG .
```

## Exec a command without entering a container

```bash
docker exec CONTAINER sh -c "cat /tmp/test"
```

## Fast Testing with alpine and docker-compose

```bash
version: "3.0"
services:
  alpine:
    image: alpine
    volumes:
      - /tmp/:/tmp/
    tty: true
````

Starting the service with `docker-compose up -d`keeps the container running

## Set docker host
```bash
DOCKER_HOST=tcp://192.168.56.101:2375
# with TLS enabled Daemon
# make sure that ~/.docker/ of the current user contains the ca.pem or the {cert,key}.pem in case of client auth
export DOCKER_TLS_VERIFY=1
```