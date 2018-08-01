---
title: ')Windows Tricks'
taxonomy:
    category:
        - Windows
    author:
        - Knecht
---

[TOC]

## Programmatically (un)set environment variables in Winodws

Use setx in a batch file.

```batch
setx NAME "value"
```

Unset (persistant) only in the registry (execute 'regedit')
```
HKEY_CURRENT_USER\Environment
```