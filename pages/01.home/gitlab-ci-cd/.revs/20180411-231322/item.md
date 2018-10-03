---
title: 'Gitlab CI-CD'
taxonomy:
    category:
        - Applications
---

## Install gitlab-runner

```bash
docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest
```
More install options are [available](https://docs.gitlab.com/runner/install/)

## Register gitlab-runner

Run in your runner host (here in the docker container)
```
sudo gitlab-runner register
```
- Get your token from `/admin/runners` of your Gitlab instance
- Set your [executioner](https://docs.gitlab.com/runner/executors/README.html) (here docker)
- No tags, allow untagged jobs, no shared runner (without those settings the runner stuck)

## Basic maven build
.gitlab-ci.yml
```yml
image: maven:latest

verify:
  stage: build
  script:
    - mvn verify

build:
  stage: build
  script:
    - mvn compile
```