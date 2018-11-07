---
title: Other
taxonomy:
    category:
        - Personal
---

[TOC]

## Install ruby gem behind a proxy
```bash
gem install <name> -p http://my.proxy.com:1234
```

## Maximize emacs (gVim xTerm,...) in KDE without gaps

- Right click on Titlebar
- More Actions -> Special Application Settings -> Size & Position -> set `Obey geometry restriction` to `Force` `No`

## Hide titlebar in maximized KDE windows

Add
```ini
[Windows]
BorderlessMaximizedWindows=true
```
to the kwin config file

KDE4:
```bash
~/[.kde|.kde4|.kdemod4]/share/config/kwinrc
```

KDE5(Plasma):
```bash
~/.config/kwinrc
```

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

## Fancy http error pages

In [my repo](https://repo.rootknecht.net/allaman/404) I collect some funky http error pages I stumbled over

## Multi row tabs in Firefox Quantum 58+

In your `userChrome.css` file in a folder `chrome` in your Firefox` profile folder (create if not existing) add the following lines:

```
.tabbrowser-tab:not([pinned]) {min-width:35px;max-width:35px;}
.tabbrowser-tab,.tab-background {height:var(--tab-min-height);}
.tab-stack {width: 100%;}
#tabbrowser-tabs .scrollbox-innerbox {display: flex;flex-wrap: wrap;}
#tabbrowser-tabs .arrowscrollbox-scrollbox {overflow: visible;display: block;}
#titlebar,#titlebar-buttonbox{height:var(--tab-min-height) !important;}
#titlebar{margin-bottom:calc(var(--tab-min-height)*-1) !important;}
#main-window[sizemode="maximized"] #titlebar{margin-bottom:calc(6px + var(--tab-min-height)*-1) !important;}
#main-window[sizemode="maximized"] #TabsToolbar{margin-left:var(--tab-min-height);}
#titlebar:active{margin-bottom:0 !important;}
#titlebar:active #titlebar-content{margin-bottom:var(--tab-min-height) !important;}
#tabbrowser-tabs .scrollbutton-up,.tabbrowser-tabs .scrollbutton-down,#alltabs-button,.tabbrowser-tab:not([fadein]){display: none;}
```
<small>[Source](https://gist.githubusercontent.com/forexhill/b0446cc31e5001c9e87754df83f0f1ca/raw/f4f1a807d43434a1f10908364dec56ecdf08422c/gistfile1.txt)</small>