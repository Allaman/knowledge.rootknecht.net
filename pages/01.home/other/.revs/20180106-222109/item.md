---
title: Other
taxonomy:
    category:
        - Others
---

[TOC]

## Install ruby gem behind a proxy
```bash
gem install <name> -p http://my.proxy.com:1234
```

## Respawn tmux pane
In tmux command mode 
```
:respawn-pane -k
```

## Maximize emacs (gVim xTerm,...) in KDE without gaps

- Right click on Titlebar
- More Actions -> Special Application Settings -> Size & Position -> set `Obey geometry restriction` to `Force` `No`

## Fix XeLatex sty or font not found errors
After installation of additional packages/fonts run
```bash
sudo texhash
```
## Fix xdvipdfmx:fatal: pdf_ref_obj(): passed invalid object.
Occurs when fontawesome is used. Add `\newfontfamily{\FA}{[FontAwesome.otf]}` after loading the fontawesome package