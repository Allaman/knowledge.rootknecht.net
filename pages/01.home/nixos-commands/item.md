---
title: 'NixOS Commands'
taxonomy:
    category:
        - Linux
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
# for example unstable channel
nix-channel --add https://nixos.org/channels/nixos-unstable nixos
nix-channel --update
```

### Remove channel
```bash
nix-channel --remove CHANNEL_ALIAS
```
### Upgrade
```bash
nixos-rebuild switch --upgrade
```
### Access NixOS config options
```bash
nixos-option OPTION-SET
nixos-option services.sshd
```

### Search package
```bash
nix-env -qaP '.*PACKAGE.*'
```
### Show package description
```bash
nix-env -qa --description '.*PACKAGE.*'
```

### Upgrade package(s)
```bash
nix-env -u PACKAGE
nix-env -u
```

### (Un)Install package
```bash
nix-env -i PACKAGE
nix-env -e PACKAGE
```

### Install package from source
```bash
nix-env -f https://github.com/NixOS/nixpkgs/archive/master.tar.gz -iA pkgs.NAME
```

### Clean system
```sh
nix-collect-garbage -d # as root to clear system profile
```

### Optimize store
```sh
nix-store --optimise
```