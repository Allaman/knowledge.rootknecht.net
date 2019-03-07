---
title: CLI
taxonomy:
    category:
        - Application
---

[TOC]

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

## grep alternatives

[Comprehensive comparison](https://beyondgrep.com/feature-comparison/) of grep alternatives.

Currently running [ripgrep](https://github.com/BurntSushi/ripgrep)

## cat alternative

[bat](https://github.com/sharkdp/bat)

- Syntax highlightning
- Git integration
- Automatic paging

## fasd

[fasd](https://github.com/clvv/fasd)

- fast navigation in your shell
- quickaccess to files, directories
- inspired by autojump, z, and v

## mu-repo

[mu-repo](http://fabioz.github.io/mu-repo/)

- manage multiple git repos
- run git commands on multiple repos

## ls alternative

[exa](https://the.exa.website/)

- fast (in rust implemented)
- coloerd multi column outpu
- respects git status

## Mount Windows Virtualbox vmdk

`ndb` (network device block) module and command `qemu-nbd` is required!

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

## Work with CSV like a boss

[xsv](https://github.com/BurntSushi/xsv)

**Search by column and output specific columns**
```sh
  xsv search -d ';' -s Role \
  inventory.csv  \
  | xsv select Hostname,Branch \
  | xsv table
```

**Join two csv tables**
```sh
xsv join -d ';' Hostname inventory.csv Hostname status.csv | xsv table
```

xsv supports many operations on csv files! Sorting, slicing, statistics, filtering, and more. Have a look at the documentation


## CLI Services

1. Weather
  ```bash
  curl wttr.in/München
  ```
1. Crypto currencies
  ```bash
  curl curl eur.rate.sx/eth
  ```
1. External IP
  ```bash
  curl ipecho.net/plain
  ```
1. Cheatsheet
  ```bash
  curl cht.sh/ls
  curl cht.sh/python/dirs+recursive
  ```
  Install cli client:
  ```bash
  curl https://cht.sh/:cht.sh > /usr/local/bin/cht.sh
  chmod +x ~/bin/cht.sh
  ```
1. Latencies
  ```bash
  curl cheat.sh/latencies
  ```
1. Generate QR codes
  ```bash
  curl qrenco.de/https://google.com
  curl qrenco.de/Hello%20World
  ```
1. URL Shortener
	```bash
	curl -s http://tinyurl.com/api-create.php\?url=https://google.com
	```
1. Translate

	[Translate Shell](https://github.com/soimort/translate-shell)

1. Random commit messages
  ```bash
  curl -sk https://whatthecommit.com/index.txt
  ```
1. Star Wars in terminal
  ```bash
  nc towel.blinkenlights.nl 23
  ```
