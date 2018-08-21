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

! Ensure that your linux user is in vboxsf group ( `sudo usermod -aG vboxsf USER`)

! Ensure that the vboxsf module is loaded (`sudo modprobe -a vboxsf`)

## Start a simple web server for testing/developing
PHP
```bash
php -S localhost:8000
```

Python
```bash
python -m SimpleHTTPServer 8000
```

JavaScript
```bash
npm install http-server –g
http-server
```

## Markdown highlighted notes
For custom highlighted notes in a normal Markdown use the following snippets
```markdown
div class="note"></div>

I am a highlighted note
```

```css
<style>
.note+p {
    padding: 8px 35px 8px 14px;
    margin-bottom: 20px;
    text-shadow: 0 1px 0 rgba(255,255,255,0.5);
    border-radius: 4px;
    color: #3a87ad;
    background-color: #d9edf7;
    border-color: #bce8f1;
}

.note+p:before {
    font-weight: bold;
    display: block;
}
</style>
```