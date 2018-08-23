---
title: Drone
taxonomy:
    category:
        - Applications
        - DevOps
        - CI/CD
    author:
        - Knecht
---

## Use Drone to scp files to a target
With [Drone-scp](http://plugins.drone.io/appleboy/drone-scp/)

Add secrets (use exact these names)
```bash
./drone secret add --repository REPO -name SSH_PASSWORD -value PASSWORD
./drone secret add --repository REPO -name SSH_KEY -value @/path/to/id_rsa
./drone secret add --repository REPO -name SSH_USERNAME -value USER
```
.drone.yml
```yaml
pipeline:
  deploy:
    image:    appleboy/drone-scp
    host:     HOST
    port:     22
    secrets: [ SSH_USERNAME, SSH_PASSWORD ]
    # secrets: [ SSH_USERNAME, SSH_KEY ]
    rm: true
    source:
      - src/
    target:
      - /var/www/html
    strip_components: 1
```