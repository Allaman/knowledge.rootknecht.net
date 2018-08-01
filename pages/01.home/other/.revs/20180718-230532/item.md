---
title: Other
taxonomy:
    category:
        - Others
    author:
        - Knecht
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

## Set tmux as login shell
In your .bashrc or zshrc
```bash
if command -v tmux>/dev/null; then
  [[ ! $TERM =~ screen ]] && [ -z $TMUX ] && exec tmux
fi
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

## Create new MySQL database and user
```bash
mysql -u root -p
create database name;
grant all privileges on database.* to 'user'@'localhost' identified by "password";
flush privileges;
```

## Mount a virtualbox shared folder in a linux guest
in `/etc/fstab`
```bash
SHARED_FOLDER_NAME /PATH/TO/MOUNT_POINT vboxsf rw,dmask=770,fmask=600,uid=1000,gid=109 0 0
```
- uid is the id of your user in the guest
- gid is the id of the vboxsf-group in the guest
- dmask sets the default permissions for directories
- fmask sets the default permissions for files 