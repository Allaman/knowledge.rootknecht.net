---
title: 'Shell Tricks'
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

[TOC]

## Auto complete a command with history-search
This setting allows you to enter shell commands quite efficient. You just enter the first couple of letters of a coomand and press page up/down. The shell tries to auto complete them based on your previous commands.

In /etc/inputrc
```bash
# alternate mappings for "page up" and "page down" to search the history
"\e[5~": history-search-backward
"\e[6~": history-search-forward
```

## Force changes to /etc/hosts
```bash
systemctl restart nscd
```

## Write multiple lines without editor

```bash
echo "line 1
line 2" >> multiple
```
or

```bash
cat <<EOT >> multiple
line 1
line 2
EOT
```

## Disable HTTPS Certificate Verification

**wget**
```bash
--no-check-certificate
```

**git**
```bash
-c http.sslVerify=false
```
or in .git/config 
```ini
[http]
sslVerify = false
```
**curl**
```bash
--insecure
```

**conda**
```bash
conda config --set ssl_verify false
```

**pip**
```bash
pip install [--index-url=http://pypi.python.org/simple/] --trusted-host pypi.python.org
```