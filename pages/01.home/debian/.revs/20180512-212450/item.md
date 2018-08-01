---
title: Debian
taxonomy:
    category:
        - Others
    author:
        - Knecht
---

[TOC]

## Apt-get upgrade
Do not add or remove dependencies
```bash
apt-get upgrade 
```
Only add new dependencies
```bash
apt-get upgrade --with-new-pkgs
```
Add and remove dependencies
```bash
apt-get dist-upgrade
```

## Fix apt-get Hashsum mismatch in Debian 9
Usually occuring behind a (enterprise) proxy setup

/etc/apt/apt.conf.d/99fixbadproxy
```
Acquire::http::Pipeline-Depth 0;
Acquire::http::No-Cache true;
Acquire::BrokenProxy    true;
```

## Different version of packages

```bash
apt-cache policy PACKAGE
apt-get install PACKAGE=VERSION
```

## Hold packages

```bash
apt-mark hold PACKAGE
apt-mark unhold PACKAGE
apt-mark showhold
```