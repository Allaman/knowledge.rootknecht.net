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

## ripgrep

ripgrep](https://github.com/BurntSushi/ripgrep)

- `grep` alternative
- written in Rust
- fast
- mostly grep compatible

[Comprehensive comparison](https://beyondgrep.com/feature-comparison/) of grep alternatives.

## bat

[bat](https://github.com/sharkdp/bat)

- `cat` alternative
- written in Rust
- Syntax highlightning
- Git integration
- Automatic paging

## fd

[fd](https://github.com/sharkdp/fd)

- `find` alternative
- written in Rust
- fast
- provides sane defaults
- does not intend to fully replace find

## fzf

[fzf](https://github.com/junegunn/fzf)

- command line fuzyy finder
- written in Golang
- endless use cases
- portable
- Integration in tmux, vim, bash, zsh, ...

## fasd

[fasd](https://github.com/clvv/fasd)

- fast navigation in your shell
- written in shell
- quickaccess to files, directories
- inspired by autojump, z, and v

## prettyping

[prettyping](https://github.com/denilsonsa/prettyping)

- wrapper around ping
- written in shell
- colorful and easy to read

## mu-repo

[mu-repo](http://fabioz.github.io/mu-repo/)

- manage multiple git repos
- run git commands on multiple repos

## exa

[exa](https://the.exa.website/)

- `ls` alternative
- written in Rust
- fast
- colored multi column output
- respects git status
- single binary

## translate-shell

[translate-shell](https://github.com/soimort/translate-shell)

- language translation in your shell
- powered by Google Translate (default) , Bing Translator, Yandex.Translate, and Apertium
- written in Awk
- self contained executable

## tig

[tig](https://github.com/jonas/tig)

- modern text interface for git
- written in C
- ncurses GUI

## trash-cli

[trash-cli](https://github.com/andreafrancia/trash-cli)

- `rm` alternative respecting the trashcan
- deleted files can be restored
- written in Python

## ngrep

[ngrep](https://github.com/jpr5/ngrep)

- user friendly `tcpdump` alternative
- written in C
- PCAP based

## xsv

[xsv](https://github.com/BurntSushi/xsv)

- CSV parsing and manipulation
- written in Rust
- indexing, slicing, analyzing, splitting and joining 

**Search by column and output specific columns**
```sh
  xsv search -d ';' -s Role \
  data.csv  \
  | xsv select Name,Location \
  | xsv table
```

**Join two csv tables and write in new csv**
```sh
xsv join -d ';' Name data.csv Name status.csv | xsv fmt -t ';' > joined.csv
```

## cheat.sh

[cheat.sh](https://github.com/chubin/cheat.sh)

- cheatsheet interface
- written in Python
- 56 programming languages, several DBMSes, and more than 1000 most important UNIX/Linux commands
- simple curl/browser interface
- fast
- CLI client `cht.sh`

## cloc

[cloc](https://github.com/AlDanial/cloc)

- count lines of code
- written in Perl
- autodetects languages
- comments agnostic

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

## fzf tweaks

[fzf](https://github.com/junegunn/fzf) is a CLI fuzzy finder with endless possibilities. If you want to improve your terminal workflow you **must** check this out.

- `export FZF_COMPLETION_TRIGGER=',,'` 

	Allows to trigger fzf after arbitrary commands, for instance `vim ,,`  <TAB> invokes fzf

- `export FZF_DEFAULT_OPTS="--bind='ctrl-o:execute:vim {} > /dev/tty'"`
	
    Enables you to directly open a file for fzf results

- `export FZF_CTRL_T_OPTS="--preview '(highlight -O ansi -l {} 2> /dev/null || cat {} || tree -C {}) 2> /dev/null | head -200'"` 

	Shows a preview of highlighted files in fzf

- `export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -200'"` 

	Directory structure preview of highlighted directories within fzf

- `command -v rg >/dev/null 2>&1 && export FZF_DEFAULT_COMMAND='rg --files --no-ignore-vcs --hidden'` 
	
    Use [ripgrep](https://github.com/BurntSushi/ripgrep) when it is installed as default

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
    See [cheat.sh](#cheat-sh)
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
1. Random commit messages
  ```bash
  curl -sk https://whatthecommit.com/index.txt
  ```
1. Star Wars in terminal
  ```bash
  nc towel.blinkenlights.nl 23
  ```
