---
title: SSH
taxonomy:
    category:
        - Shell
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