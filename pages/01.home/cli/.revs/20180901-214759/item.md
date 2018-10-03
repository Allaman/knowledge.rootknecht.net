---
title: CLI
taxonomy:
    category:
        - Shell
        - tools
---

## htop

[htop](https://hisham.hm/htop/) is a enhanced version of `top` which comes preinstalled on most systems.
- *P* &rarr; sort by CPU
- *M* &rarr; sort by memory usage
- *F4* &rarr; filter processes by string
- *space* &rarr; mark a single process

Settings are stored in `$HOME/.config/htop/htoprc` but overwritten by the application by pressing `F10` save and exit.

## diff-so-fancy
[diff-so-fancy](https://github.com/so-fancy/diff-so-fancy) is an alternative customazable very nice looking diff tool for `git diff`.

In your git config:
```ini
[pager]
   diff = diff-so-fancy | less --tabs=1,5 -RFX
   show = diff-so-fancy | less --tabs=1,5 -RFX    
```