---
title: 'Mixed Content'
taxonomy:
    category:
        - Uncategorized
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
```sql
mysql -u root -p
create database name;
grant all privileges on database.* to 'user'@'localhost' identified by "password";
flush privileges;
```

## Export all mysql tables to csv files

```bash
mysqldump ovs -u root -p -T /path/to/folder --fields-terminated-by=,
```
The target folder must be writeable from the mysql process user

## Check mysql/mariadb user and auth

```sql
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

## Create mysql backup user (read-only)

```mysql
GRANT SELECT,LOCK TABLES ON DBNAME.* TO 'backup'@'localhost';
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

## Print info pages to pdf

```bash
info --subnodes -o - groff | enscript -o - | ps2pdf - groff.pdf
```

## Dell iDrac virtual console network dropped

In `/usr/lib/jvm/java-8-openjdk/jre/lib/security/java.security` (or the appropriate path) adjust
```bash
jdk.tls.disabledAlgorithms=SSLv3, RC4, MD5withRSA, DH keySize < 1024, \
EC keySize < 224, DES40_CBC, RC4_40
```


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

## Humble Bumble eBook bulk download

Paste and execute in the dev tools of the browser

```javascript
// How many seconds to delay between downloads.
var delay = 1000;
// whether to use window.location or window.open
// window.open is more convenient, but may be popup-blocked
var window_open = false;
// the filetypes to look for, in order of preference.
// Make sure your browser won't try to preview these filetypes.
var filetypes = ['epub', 'mobi', 'pdf'];

var downloads = document.getElementsByClassName('download-buttons');
var i = 0;
var success = 0;

function download() {
  var children = downloads[i].children;
  var hrefs = {};
  for (var j = 0; j < children.length; j++) {
    var href = children[j].getElementsByClassName('a')[0].href;
    for (var k = 0; k < filetypes.length; k++) {
      if (href.includes(filetypes[k])) {
        hrefs[filetypes[k]] = href;
        console.log('Found ' + filetypes[k] + ': ' + href);
      }
    }
  }
  var href = undefined;
  for (var k = 0; k < filetypes.length; k++) {
    if (hrefs[filetypes[k]] != undefined) {
      href = hrefs[filetypes[k]];
      break;
    }
  }
  if (href != undefined) {
    console.log('Downloading: ' + href);
    if (window_open) {
      window.open(href);
    } else {
      window.location = href;
    }
    success++;
  }
  i++;
  console.log(i + '/' + downloads.length + '; ' + success + ' successes.');
  if (i < downloads.length) {
    window.setTimeout(download, delay);
  }
}
```
<small>[Source](http://shallowsky.com/blog/tech/web/downloading-from-humble-bundle.html)</small>