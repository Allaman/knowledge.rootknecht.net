---
title: Git
taxonomy:
    category:
        - Others
---

[TOC]

## Change remote of an existing repo
Check current urls:
```bash
git remote -v
```
Switch urls:
```bash
git remote set-url origin NEWURL
```
Compare change
```bash
git remote -v
```
Push to new remote
```bash
git push -u origin master
```

## Run git command over all subdirectories

```bash
find . -maxdepth 1 -type d -exec git --git-dir={}/.git --work-tree=$PWD/{} pull \;
```

## Git proxy
```bash
git config --global http.proxy http://proxy.company.com:3128
```
or in .git/config
```
[http]
	proxy = http://proxy.company.com:3128
```
or temporarly as command line argument
```bash
-c http.proxy http://proxy.company.com:3128
````

## Use Github and Gitlab
### Use multiple remotes named differently
```bash
git remote add github https://github.com/USER/repo.git
git push/pull origin
git push/pull github
```
When the origin is at github vice versa.

### Single remote with multiple targets
```bash
git remote set-url –add origin https://github.com/USER/repo.git
git push/pull origin
```
When the origin is at github vice versa. Now, origin will targed the Gitlab as well as Github remotes