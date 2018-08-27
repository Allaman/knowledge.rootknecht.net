---
title: 'Git Tricks'
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
oder in .git/config
```
[http]
	proxy = http://proxy.company.com:3128
```

## Gitignore for latex projects
[gitignore](latex.gitignore)