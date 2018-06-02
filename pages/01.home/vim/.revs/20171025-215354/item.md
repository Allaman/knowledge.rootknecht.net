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

## Modeline
By setting `set modeline=1` you can enable the [Modeline Magic](http://vim.wikia.com/wiki/Modeline_magic). When it is not working you can check the setting with the following command:
```
:verbose set modeline?
```
Some distros disable it with `nomodeline` in /etc/vimrc
