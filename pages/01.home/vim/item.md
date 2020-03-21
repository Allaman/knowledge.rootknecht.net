---
title: Vim
taxonomy:
    category:
        - Application
---

[TOC]

## My (Neo)Vim config

[vimrc](https://repo.rootknecht.net/allaman/public-dotfiles/blob/master/vimrc)

## Safe file opend by an user as root
```
:w !sudo tee %
```

## Delete empty lines

```
:g/^$/d
```

## Replace currently selected text with default register without yanking it
```
vnoremap p "_dP
```

## Open file in binary mode
```bash
vim -b
```

## Add string at the end of lines

- `SHIFT-v` to select lines
- `:norm Astring'

norm means `type the following commands` and the `A` stands for append

## Add string at the start of lines

- `^` to move to the start of the line
- `CTRL-v' to block select your lines
- `SHIFT-I` to insert your string (on *one* line)
- `ESC` to insert the string on all lines

## Open multiple files in vim tabs
```bash
vim -p [file1] [file2] ...
```

## Convert line endings

```sh
vim +':w ++ff=unix' +':q' FILE
```

or for other endings

- `:w ++ff=dos`
- `:w ++ff=mac`

## Show mappings

```
:map [<C-j>]
:verbose map [<C-j>]
```

## Print infos (within) vim
Prints various information about vim like version, enabled features, compile flags and loaded configuration files.
```
:version
```

## Folding

- **za**: Toogle at the current line
- **zo**: Open fold
- **zc**: Close fold
- **zR**: Open all folds
- **zM**: Close all folds
- **zm**: Increases the foldlevel by one
- **zr**: Decreases the foldlevel by one
- **zj** Moves the cursor to the next fold
- **zk**: Moves the cursor to the previous fold
- **\[z**: Move to start of open fold
- **]z**: Move to end of open fold
- **zf#j**: Creates a fold from the cursor down # lines
- **zf/string** Creates a fold from the cursor to string
- **zd**: Deletes the fold at the cursor
- **zE**: Deletes all folds

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

## Quickfix window

```bash
:ccl[ose]
:cope[n]
:cp
:cn
```

## Location window

```bash
:lcl[ose]
:lop[en]
:lp
:ln
```

## Use CAPS as ESC

In Linux use `setxkbmap`:

```bash
setxkbmap -option caps:escape # More options available
setxkbmap -option # to reset changes
```

## NeoVim and vimrc

In `.config/nvim/init.vim` (create if not existing)

```
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath=&runtimepath
source ~/.vimrc
```

## Enter copyright symbol

1. In insert mode
2. `C-k` a question mark will appear
3. Enter `Co`

[Here](https://devhints.io/vim-digraphs) is a cheatsheet about digraphs (how this is called)

## Tabs vs buffers
    A buffer is the in-memory text of a file.
    A window is a viewport on a buffer.
    A tab page is a collection of windows.
