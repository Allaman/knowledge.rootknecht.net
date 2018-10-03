---
title: 'NixOS Configuration'
taxonomy:
    category:
        - NixOS
---

The main config file of NixOS is `/etc/nixos/configuration.nix`. After each modification the changes must be propagate to the system (see [NixOS Commands](../nixos-commands)).

## Syntax of configuration.nix
`{ config, pkgs, ... }:` defines a function with at least to arguments returning `{ option definitions}` which are a set of `name = value` pairs.

Example for enabling apache2 service
```
{ config, pkgs, ... }:

{ services.httpd.enable = true;
  services.httpd.adminAddr = "alice@example.org";
  services.httpd.documentRoot = "/webroot";
}
```
which is equal to
```
{ config, pkgs, ... }:

{ services = {
    httpd = {
      enable = true;
      adminAddr = "alice@example.org";
      documentRoot = "/webroot";
    };
  };
}
```
! Dots in option names are shorthand for a set containing another set

Options have a specified type. The most important are:
1. Strings
	
    `networking.hostName = "dexter";`. 
    Special characters need to be escaped with `\`. Multi-line strings are enclosed with double single quotes, e.g.
    ```
    networking.extraHosts =
        ''
            127.0.0.2 other-localhost
            10.0.0.1 server
        '';
    ```
1. Booleans
	
    Can be true or false, e.g. `networking.firewall.enable = true;`
1. Integers
	
    `boot.kernel.sysctl."net.ipv4.tcp_keepalive_time" = 60;`.
    Here, net.ivp4 is enclosed in quotes to prevent it from being interprated is set of sets. This is just the name of the kernel option
    
1. Sets

	```
        fileSystems."/boot" =
      { device = "/dev/sda1";
        fsType = "ext4";
        options = [ "rw" "data=ordered" "relatime" ];
      };
	```
    
1. Lists

	`boot.kernelModules = [ "fuse" "kvm-intel" "coretemp" ];`.
    Note that elements are separated by whitespaces and can be of any type, e.g. sets `swapDevices = [ { device = "/dev/disk/by-label/swap"; } ];`
    
1. Packages

	```
      environment.systemPackages =
      [ pkgs.thunderbird
        pkgs.emacs
      ];

    postgresql.package = pkgs.postgresql90;
```

! A comprehensive list of options can be found at [NixOS options](https://nixos.org/nixos/options.html).

## Enable automatic updates
```
system.autoUpgrade.enable = true;
```

## Add new user
```
  users.extraUsers.USERNAME = {
    createHome = true;
    home = "/home/user";
    extraGroups = [ "wheel" ];
    shell = pkgs.bashInteractive;
    openssh.authorizedKeys.keys = [ "ssh-rsa ..." ];
    uid = 1000;
  };
```
This user has no password and is only able to login with its private ssh key. In order to use `sudo -i` a pasword is required. To set a password loin as root und execute `passwd USERNAME`. 