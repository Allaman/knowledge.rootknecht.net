---
title: SSH
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

## Basic usage with custom port and custom key
```bash
ssh -i ~/.ssh/id_rsa -p PORT USER@HOST
```

## Local port forwarding
```bash
ssh -L BINDADDRESS:PORT:DSTHOST:DSTPORT USER@HOST
```

## Remote port forwarding
```bash
ssh -R BINDADDRESS:PORT:LOCALHOST:LOCALPORT USER@HOST
```

## Run command on host
```bash
ssh -i ~/.ssh/id_rsa USER@HOST "sudo apt-get update && sudo apt-get upgrade"
```

## SSH related files
|File|Purpose|
|------------|
|~/.ssh/|User specific ssh settings|
|~/.ssh/authorized_keys|Public keys which are allowed to login as this user|
|~/.ssh/config|User specific ssh config file|
|~/.ssh/id_\*|Common prefix for public/private ssh keys|
|~/.ssh/known_hosts|Public host keys known to user|
|/etc/ssh/ssh_config|Global ssh client config|
|/etc/ssh/sshd_config|Global ssh server config|

## Add authorized key
```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
#  remotley
ssh-copy-id -i ~/.ssh/id_rsa USER@HOST
```

## Copy files
**From host**
```bash
scp USER@HOST:/path/to/file.txt /tmp/file.txt
```
**To host**
```bash
scp /tmp/file.txt USER@HOST:/tmp/file.txt
```
**Options**
- /-r/ copy recursive
- /-P/ custom port (note capital P in contrast to ssh)