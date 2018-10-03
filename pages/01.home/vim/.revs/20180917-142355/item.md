---
title: Vim
taxonomy:
    category:
        - Application
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

## Startup time
```bash
vim --startuptime vim.log
```

## Open vim in debug mode
```bash
vim -D
```

## Use CAPS as ESC

In Linux use `setxkbmap`:

```bash
setxkbmap -option caps:escape # More options available
setxkbmap -option # to reset changes
```

## Enter copyright symbol

1. In insert mode
2. `C-k` a question mark will appear
3. Enter `Co`

[Here](https://devhints.io/vim-digraphs) is a cheatsheet about digraphs (how this is called)