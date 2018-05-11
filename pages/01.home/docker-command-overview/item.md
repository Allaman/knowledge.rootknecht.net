---
title: 'Docker Command Overview'
taxonomy:
    category:
        - Docker
        - DevOps
    author:
        - Knecht
---

[TOC]

! See [Full CLI reference](https://docs.docker.com/engine/reference/commandline/docker/#child-commands) for a comprehensive documentation

## Getting information
|Command|Result|
|---|---|
|docker version|Get version info about docker|
|docker info|Get overview of different docker info|
|docker ps|List running containers|
|docker ps -a|List all existing containers|
|docker system df|Get storage usage of Docker|
|docker system top|Get running process of a container|
|docker stats|List live stream of container usage

## Managing volumes
|Command|Result|
|---|---|
|docker volume ls| List all docker volumes|
|docker volume inspect *VOLUME-ID*|List detailed volume information|

## Managing images
|Command|Result|
|---|---|
|docker image ls|List local images|
|docker rmi *IMAGE-ID*|Remove specified image|
|docker image prune|Remove unused images|
|docker image prune -a|Remove all images|

## Managing container
|Command|Result|
|---|---|
|docker exec -it *CONTAINER-ID* [bash\|sh]|Log into the container|
|docker exec *CONTAINER-ID* *command*|Executes command in the container|

## Clean up
|Command|Result|
|---|---|
|docker stop $(docker ps)|Stops all running containers|
|docker rm $(docker ps -q)|Removes all containers|
|docker rm $(docker image ls -q)|Deletes all images|

Alternative for Docker API 1.25 and greater:

|Command|Result|
|---|---|
|docker system prune| Removes unused data|
|docker system prune -a| Removes unused data but not just dangling images|



