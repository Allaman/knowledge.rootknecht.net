---
title: 'NixOS Commands'
taxonomy:
    category:
        - NixOS
    author:
        - Knecht
---

## Configuration
### Activate your configuration but not reboot persistant
```bash
nixos-rebuild test
```
### Activate your configuration not before reboot
```bash
nixos-rebuild boot
```
### Activate your configuration and make it permanent
```bash
nixos-rebuild switch
```
### List automatic tasks
```bash
systemctl list-timers
```

## Updates/Upgrades
### See subscribed channels
```bash
nix-channel --list | grep nixos
```
### Switch channel
! Channels are per user so switching a channel as user will not affect the main config!
```bash
nix-channel --add https://nixos.org/channels/channel-name nixos
```
### Upgrade
```bash
nixos-rebuild switch --upgrade
```