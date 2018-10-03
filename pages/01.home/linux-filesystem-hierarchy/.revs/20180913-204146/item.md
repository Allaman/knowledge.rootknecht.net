---
title: 'Linux Filesystem Hierarchy'
taxonomy:
    category:
        - Linux
---

[FHS](https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/)
```bash
/
├── bin
├── boot
├── dev
├── etc
├── home
├── initrd
├── lib
├── lib64
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv 
├── usr 
│   ├── bin 
│   ├── include 
│   ├── lib 
│   ├── lib64
│   ├── local 
│   ├── sbin 
│   ├── share 
│   ├── src 
└── var 
└── tmp 
```

[FHS](https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/)
- bin

useful commands that are of use to both the system administrator as well as on-privileged users, e.g. cat, chmod, cp, echo, pwd, rm, sed, ...
- boot

everything required for the boot process except for configuration files not needed at boot time
- dev

special or device files. Hard drives and DVD drives are block devices. Serial ports, parallel ports are character devices.
- etc

contains all system related configuration files defined as local files used to control the operation of a program which must be static and cannot be an executable binary.
- home

each user is also assigned a specific directory that is accessible only to them and the system administrator which are subdirectories of /home
- initrd

capability to load a RAM disk by the boot loader
- lib
- lib64

contains kernel modules and those shared library images needed to boot the system and run the commands in the root filesystem like /bin and /sbin
- media

containing mount points for removable media
- mnt

generic mount point for filesystems or devices
- opt

reserved for all the software and add-on packages that are not part of the default installation
- proc

virtual filesystem. Sometimes referred to as a process information pseudo-file system. Contains runtime system information (e.g. system memory, devices mounted, hardware configuration, etc). Can be regarded as a control and information centre for the kernel. 
- root

Home directory of the root account
- run
- sbin

contains only binaries essential for booting, restoring, recovering, and/or repairing the system in addition to the binaries in /bin, e.g. fdisk, init, route, swapof, 
- srv

contains site-specific data which is served by this system.
- usr  ("user system resources")
    - *bin*  &rarr; vast majority of binaries
    - *include* &rarr; 'header files', needed for compiling user space source code.
    - *lib* &rarr; contains program libraries.
    - *lib64*
    - *local* &rarr; self-compiled or third-party programs safe from being overwritten by system updates
    - *sbin* &rarr; contains programs for administering a system, meant to be run by 'root', e.g. chroot, useradd
    - *share* &rarr; contains 'shareable', architecture-independent files (man pages, icons, fonts etc)
    - *src* &rarr; contains the Linux kernel sources, header-files and documentation.

- var

Contains variable data like system logging files, mail and printer spools, and temporary files.
- tmp 

files that are required temporarily