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