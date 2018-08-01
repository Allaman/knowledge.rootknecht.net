---
title: 'Vim Tricks'
taxonomy:
    category:
        - Vim
    author:
        - Knecht
---

[TOC]

## Safe file opend by an user as root
```vimscript
:w !sudo tee %
```

## Open file in binary mode
```bash
vim -b
```

## Open multiple files in vim tabs
```bash
vim -p [file1] [file2] ...
```

## Print infos (within) vim
Prints various information about vim like version, enabled features, compile flags and loaded configuration files.
```
:version
```