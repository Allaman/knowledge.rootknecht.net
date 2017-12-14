---
title: 'NixOS Installation'
taxonomy:
    category:
        - NixOS
    author:
        - Knecht
---

This article describes a simple *not* heavily customized installation of NixOS (nixos-minimal-17.09.1756.c99239bca0-x86_64-linux.iso) on a clean vServer.

## ISO
We download the iso image from the [official Homepage](https://nixos.org/nixos/download.html) and mount it as boot device in our virtual machine (usually through a admin panel of your provider).
! There are also some other install methods. At the time writing this namely AWS, Azure, and OVA.

## Installation
### Preparation
Setting a german keyboard layout with `loadkeys de` was not working but we will access the live image within ssh anyway as the web panel of my machine from my provider is not very convienient. We must set a password for the root user (which is empty initially) and start the ssh daemon:
```bash
passwd # set password for current user
systemctl start sshd
```
Now we are able to ssh into our booted iso image and benefit from the better usability.

### Partitioning
First, we must create a (simple) partitioning layout.
```bash
fdisk /dev/sda
-> o new dos partitioning table
-> n new primary partition (will be /)
-> n new primary partition (will be swap)
-> w write changes
```
Now we create the filesystem
```bash
mkfs.ext4 -L nixos /dev/sda1
mkfs.ext4 -L nixos /dev/sda1
```
and mount the fileystem were we gonna install NixOS
```bash
mount /dev/disk/by-label/nixos /mnt
```
We enable our swap partition with `swapon /dev/disk/by-label/swap`

### NixOS Configuration
In order to install NixOS we need to create a initial configuration skeleton with `nixos-generate-config --root /mnt`. We can adjust the settings in `/mnt/etc/nixos/configuration.nix`. In my case I changed the follwoing lines:
```
# Path where the bootloader shoud be installed
boot.loader.grub.device = "/dev/sda";
# german keyboard but english system language
i18n = {
  consoleFont = "Lat2-Terminus16";
  consoleKeyMap = "de";
  defaultLocale = "en_US.UTF-8";
};
# My timezone
time.timeZone = "Europe/Berlin";
# additional packages to be installed
environment.systemPackages = with pkgs; [
  wget vim curl htop
];
# add sshd and allow root login for further config
services.openssh = {
  enable = true;
  permitRootLogin = "yes";
};
```

### Installation
Simple do a `nixos-install` which will last only a minute or so and asks for the root password. After a reboot NixOS should start and you can login with the root account through ssh.





