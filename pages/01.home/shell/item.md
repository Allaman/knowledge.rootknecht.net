---
title: Shell
media_order: shell-startup-order.png
taxonomy:
    category:
        - Linux
---

[TOC]

## Auto complete a command with history-search
This setting allows you to enter shell commands quite efficient. You just enter the first couple of letters of a coomand and press page up/down. The shell tries to auto complete them based on your previous commands.

In /etc/inputrc
```bash
# alternate mappings for "page up" and "page down" to search the history
"\e[5~": history-search-backward
"\e[6~": history-search-forward
```

## Force changes to /etc/hosts
```bash
systemctl restart nscd
```

## Write multiple lines without editor

```bash
echo "line 1
line 2" >> multiple
```
or

```bash
cat <<EOT >> multiple
line 1
line 2
EOT
```

## Disable HTTPS Certificate Verification

**wget**
```bash
--no-check-certificate
```

**curl**
```bash
--insecure
```

## Create user with predefined password
```bash
useradd -p $(openssl passwd -1 $PASS) $USER
```

## Generate hash for passwords
```bash
echo "password" | sha1sum
```

## Add existing user to group
```bash
usermod -a -G group user
```

## Copy permissions from existing file
```bash
chown --reference=otherfile newFile
chmod --reference=otherfile newFile
```

## Modify ownership of symlinks
```bash
chown -h USER:GROUP SYMLINK
```

## Inherit permissions from parent directory
```bash
chmod g+s /path/to/parent
```

## Curl for REST API
**Auth**
```bash
# Auth with username password and store cookie information
curl -c cookies.txt -X POST -d 'username=admin&password=admin' https://example.com/login
# Use cookie auth information to post data from json file
curl -b cookies.txt -d @data.json -H "Content-Type: application/json" -X POST https://example.com/rest
# Use auth token
curl -H "X-Auth-Token: <Token ID>" https://example.com/login
```
**GET**
```bash
curl -H "Accept:application/json" https://httpbin.org/get
```
**POST**
```bash
curl \
-h "Content-type: application/json" \
-X POST \
-d '{"title": "Test Title", "note": "Test note"}' \
https://httpbin.org/
```

## Reduce size of pdf files with ghostscript

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=OPTION -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```
common options for dPDFSETTINGS are:

- dPDFSETTINGS=/screen lower quality, smaller size.
- dPDFSETTINGS=/ebook for better quality, but slightly larger pdfs.
- dPDFSETTINGS=/prepress output similar to Acrobat Distiller "Prepress Optimized" setting
- dPDFSETTINGS=/printer selects output similar to the Acrobat Distiller "Print Optimized" setting
- dPDFSETTINGS=/default selects output intended to be useful across a wide variety of uses, possibly at the expense of a larger output file

## Run multiple commands in background

```bash
(command1 &) && (command2 &)
```
## Get RAM usage

```sh
ps -o pid,user,%mem,command ax | sort -b -k3 -r
```

## Execute command as different user

```sh
su - targetuser -s /bin/bash -c "/bin/echo hello world" 
```

## Shows what is in file 2 but not in file 1

```bash
grep -v -F -x -f
```

## Merge all pdf files in current directory

```bash
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=merged.pdf *.pdf
```

## Generate handout from given pdf file

```bash
pdfjam --nup 2x3 --frame true --noautoscale false --delta "0.2cm 0.3cm" --scale 0.95
```

## Get BIOS version

```bash
sudo dmidecode | grep BIOS
```

## Get external IP

```bash
echo $(curl -ss http://ipecho.net/plain)
```

## Find primary network interface

```sh
route -n | awk '($1 == "0.0.0.0") { print $NF }'
```

## Get IP from interface

```sh
ip addr show eth0 | grep "inet\b" | awk '{print $2}' | cut -d/ -f1
ifconfig eth0 | grep "inet addr" | cut -d ':' -f 2 | cut -d ' ' -f 1
```

## Get system information

Basics e.g. modelnumber, manufactorer
```bash
dmidecode -t1
```

Ram slots
```bash
dmidecode -t memory
```

## Shell Boot Order

![](shell-startup-order.png?link&cropResize=300,300)

<small>from [here](https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html)</small>

## Zsh sourcing

* zsh always sources '~/.zshenv'. 
* Interactive shells source `~/.zshrc`
* Login shells source `~/.zprofile` and `~/.zlogin`

## Types of shells

1. Interactive

	Interactive means that the commands are run with user-interaction from keyboard, so the shell can prompt the user to enter input.

1. Non-interactive

	The shell is probably run from an automated process so it can't assume if can request input or that someone will see the output.

1. Login

	Means that the shell is run as part of the login of the user to the system. Typically used to do any configuration that a user needs/wants to establish his work-environment.

1. Non-login

	Any other shell run by the user after logging on, or which is run by any automated process which is not coupled to a logged in user.

## Custom ps command

```bash
ps axo user:20,pid,pcpu,pmem,vsz,rss,tty,stat,start,time,comm
```

## Download whole website with wget

```bash
wget \
     --recursive \
     --no-clobber \
     --page-requisites \
     --html-extension \
     --convert-links \
     --restrict-file-names=windows \
     --domains example.com \
     --no-parent \
         www.example.com/home/wiki/
```

## zip folder with password

```bash
zip -rP PASSWORD file.zip folder/
```


## PHP modules

```bash
php -m
```
/etc/php/php.ini

## Print the value of an alias

```bash
type ALIAS
```

## Convert svg to all in one icon

```bash
convert -density 384 NAME.svg -define icon:auto-resize NAME.ico
```

## Kill process by name in one line

I want to match not just only the program but its arguments (here for entr)

```bash
ps ax | grep "xelatex main.tex" | grep -v grep | awk '{print "kill -9 " $1}' | sh
```

## Rsync

This command recursively syncs two folders with advanced matching options I am running for syncing my documents to my [eInk Reader](https://onyxboox.com/boox_novapro).

```sh
rsync -rv \
--omit-dir-times \ # ignore timestamps
--prune-empty-dirs \ # don't create emtpy directories
--delete \ # also delete files at the destination
--exclude='dir1' --exclude='dir2' \ # exclude dir1 and dir2
--include='*/' \ # but include all other directories
--exclude='.*' \ # exclude all hidden files
--include='*.pdf' --include='*.epub' \ # include .pdf and .epub files
--exclude='*' \ # exclude all the rest
-e "ssh -p8022" \ # copy over ssh
source \ # source directory to sync
user@host:/destination # target directory on remote
```

## Show dd status

1. with builtin methods
    ```bash
    watch -n 3 'kill -USR1 $(pgrep "^dd$")'
	```
1. with package pv
	```bash
    dd if=/dev/urandom | pv | dd of=/dev/null
	```
    use pv -s 4G for ETA, here approximately 4G
1. with new status
	```bash
	dd if=/dev/urandom of=/dev/null status=progress
    ```
    
## Inline file returning

instead of 
```sh
grep string1 file1 > result1
grept string1 file2 > result
diff result1 result2 
```
use `<()`
```sh
diff <(grep string1 file1) <(grep string1 file2)
```

## Mount Windows Virtualbox vmdk

`ndb` (network device block) module and `qemu-nbd` command is required!

```bash
#!/bin/bash

for i in "$@"
do

case $i in
    -m|--mount)
        echo "modprobe nbd, creating device and mounting"
        sudo rmmod nbd
		sudo modprobe nbd max_part=63
        sudo qemu-nbd -c /dev/nbd0 '~/path/to/disk.vmdk'
        echo "Device created"
		if [[ -f /dev/nbd0p1 ]]
		then
			sudo mount /dev/nbd0p1 ~/mounts/tmp
		else
			sudo partprobe /dev/nbd0
			sudo mount /dev/nbd0p1 ~/mounts/tmp
		fi
        echo "Mounted at ~/mounts/tmp"
        shift
        ;;
    -u|--umount)
        echo "Unmounting, deleting device and removing nbd module"
        sudo umount ~/mounts/tmp
        sudo qemu-nbd -d /dev/nbd0
        sudo rmmod nbd
        shift
        echo "Done"
        ;;
    \?)
        echo "invalid option"
esac

done
```