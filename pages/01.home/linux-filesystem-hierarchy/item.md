---
title: 'Linux Filesystem Hierarchy'
---

[FHS](https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/)
```bash
/
# useful commands that are of use to both the system administrator as well as on-privileged users, e.g. cat, chmod, cp, echo, pwd, rm, sed, ...
├── bin
# everything required for the boot process except for configuration files not needed at boot time
├── boot
# special or device files. Hard drives and DVD drives are block devices. Serial ports, parallel ports are character devices.
├── dev
# contains all system related configuration files defined as local files used to control the operation of a program which must be static and cannot be an executable binary.
├── etc
# each user is also assigned a specific directory that is accessible only to them and the system administrator which are subdirectories of /home
├── home
# capability to load a RAM disk by the boot loader
├── initrd
# contains kernel modules and those shared library images needed to boot the system and run the commands in the root filesystem like /bin and /sbin
├── lib
├── lib64
# containing mount points for removable media
├── media
# generic mount point for filesystems or devices
├── mnt
# reserved for all the software and add-on packages that are not part of the default installation
├── opt
# virtual filesystem. Sometimes referred to as a process information pseudo-file system. Contains runtime system information (e.g. system memory, devices mounted, hardware configuration, etc). Can be regarded as a control and information centre for the kernel. 
├── proc
# Home directory of the root account
├── root
├── run
# contains only binaries essential for booting, restoring, recovering, and/or repairing the system in addition to the binaries in /bin, e.g. fdisk, init, route, swapof, 
├── sbin
├── srv # ontains site-specific data which is served by this system.
# contains user-land programs and data (as opposed to 'system land' programs and data)
├── usr # "user system resources"
│   ├── bin # vast majority of binaries
│   ├── include # 'header files', needed for compiling user space source code.
│   ├── lib # contains program libraries.
│   ├── lib64
│   ├── local # self-compiled or third-party programs safe from being overwritten by system updates
│   ├── sbin # contains programs for administering a system, meant to be run by 'root', e.g. chroot, useradd
│   ├── share # contains 'shareable', architecture-independent files (man pages, icons, fonts etc)
│   ├── src # contains the Linux kernel sources, header-files and documentation.
└── var # Contains variable data like system logging files, mail and printer spools, and temporary files.
└── tmp # files that are required temporarily
```