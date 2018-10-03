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

## Fancy error page
```html
<h1>Segmentation Fault!</h1>
<section class="error-container">
  <span><span>4</span></span>
  <span>0</span>
  <span><span>4</span></span>
</section>
<div class="link-container">
  <a target="_blank" href="mailto:support@example.com" class="more-link">Report!</a>
</div>
<style>

</style>
```

```css
.error-container {
  text-align: center;
  font-size: 180px;
  font-weight: 800;
  margin: 20px 15px;
}
.error-container > span {
  display: inline-block;
  line-height: 0.7;
  position: relative;
  color: #FFB485;
}
.error-container > span > span {
  display: inline-block;
  position: relative;
}
.error-container > span:nth-of-type(1) {
  perspective: 1000px;
  perspective-origin: 500% 50%;
  color: #F0E395;
}
.error-container > span:nth-of-type(1) > span {
  transform-origin: 50% 100% 0px;
  transform: rotateX(0);
  animation: easyoutelastic 8s infinite;
}

.error-container > span:nth-of-type(3) {
  perspective: none;
  perspective-origin: 50% 50%;
  color: #D15C95;
}
.error-container > span:nth-of-type(3) > span {
  transform-origin: 100% 100% 0px;
  transform: rotate(0deg);
  animation: rotatedrop 8s infinite;
}
@keyframes easyoutelastic {
  0% {
    transform: rotateX(0);
  }
  9% {
    transform: rotateX(210deg);
  }
  13% {
    transform: rotateX(150deg);
  }
  16% {
    transform: rotateX(200deg);
  }
  18% {
    transform: rotateX(170deg);
  }
  20% {
    transform: rotateX(180deg);
  }
  60% {
    transform: rotateX(180deg);
  }
  80% {
    transform: rotateX(0);
  }
  100% {
    transform: rotateX(0);
  }
}

@keyframes rotatedrop {
  0% {
    transform: rotate(0);
  }
  10% {
    transform: rotate(30deg);
  }
  15% {
    transform: rotate(90deg);
  }
  70% {
    transform: rotate(90deg);
  }
  80% {
    transform: rotate(0);
  }
  100% {
    transform: rotateX(0);
  }
}

h1 {
  text-align: center;
  margin: 30px 15px;
}
.zoom-area {
  max-width: 490px;
  margin: 30px auto 30px;
  font-size: 19px;
  text-align: center;
}
.link-container {
  text-align: center;
}
a.more-link {
  text-transform: uppercase;
  font-size: 16px;
  background-color: #aaa;
  padding: 10px 15px;
  border-radius: 5;
  color: #fff;
  display: inline-block;
  margin-right: 5px;
  margin-bottom: 5px;
  line-height: 1.5;
  text-decoration: none;
  margin-top: 50px;
  letter-spacing: 1px;
}
```
Adopted from https://codepen.io/ricardpriet/pen/MOKEam