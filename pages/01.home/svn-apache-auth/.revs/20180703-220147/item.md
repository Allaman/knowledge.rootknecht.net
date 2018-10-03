---
title: SVN+Apache+Auth
taxonomy:
    category:
        - Applications
---

Setup SVN accessable through Apache with authentication and authorization

## Create svn repo
```bash
svnadmin create path/to/repo
chown -R www-data:www-data path/to/repo # adjust apache user if needed
# optionally dump and import existing repo
svnadmin dump file:///path/to/exisitngt > repo.dump
svnadmin load /path/to/repo < repo.dump
```

## Setup Apache
Install/enable `mod_dav` and 

