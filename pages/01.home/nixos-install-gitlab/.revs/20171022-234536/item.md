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

## Install openssl and generate certificates
Add `openssl` to `environment.systemPackages`
`openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365`