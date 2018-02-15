---
title: 'Docker Tricks'
taxonomy:
    category:
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