---
title: 'NixOS Install Gitlab'
taxonomy:
    category:
        - NixOS
    author:
        - Knecht
---

## Install docker service

Add `virtualisation.docker.enable = true;` and optionally `extraGroups= [ "docker" ]` to a user who needs to control docker to your configuration.nix file. 

## Install docker-compose
Add `python36Packages.docker_compose` to `environment.systemPackages`

## Open firewall ports
`networking.firewall.allowedTCPPorts = [ 80 443 ]`

## Create docker-compose.yml
! Adjust paths and ports according to your setup
```docker
version: '2'

services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    restart: always
    hostname: 'gitlab'
    ports:
      - '80:80'
      - '443:443'
      - '50222:22'
    volumes:
      - '/srv/gitlab/config:/etc/gitlab'
      - '/srv/gitlab/logs:/var/log/gitlab'
      - '/srv/gitlab/data:/var/opt/gitlab'
```
Run `docker-compose up -d` to start the service in the backgroud. You should now be able to access gitlab with your machine's IP

## Install openssl and generate certificates
Add `openssl` to `environment.systemPackages`
`openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365`

## Gitlab configuration
The main configuration file is `/srv/gitlab/config/gitlab.rb` (adjust your path according to your docker-compose file)
### Enable https
In gitlab.rb put 'external_url "https://gitlab.example.com"'. Gitlab will look after your certificates according to your hostname - here `/etc/gitlab/ssl/gitlab.example.com.key` and `/etc/gitlab/ssl/gitlab.example.com.crt`.
! Note that this is the path inside of the container - on your docker host the correct path is `/srv/gitlab/config/ssl/`
Create the ssl directory and copy your previously generated files `cert.pem` and `cert.key` to this folder and rename them. The cert.pem file is the .crt file and the key.pem the .key file.