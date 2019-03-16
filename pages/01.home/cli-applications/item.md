---
title: 'CLI Applications'
taxonomy:
    category:
        - Application
---

[TOC]

## bat

[bat](https://github.com/sharkdp/bat)

- `cat` alternative
- written in Rust
- Syntax highlightning
- Git integration
- Automatic paging

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

## diff-so-fancy

[diff-so-fancy](https://github.com/so-fancy/diff-so-fancy) 

- alternative customizable nice looking diff tool for `git diff`
- written in Perl

In your git config:
```ini
[pager]
   diff = diff-so-fancy | less --tabs=1,5 -RFX
   show = diff-so-fancy | less --tabs=1,5 -RFX
```

## exa

[exa](https://the.exa.website/)

- `ls` alternative
- written in Rust
- fast
- colored multi column output
- respects git status
- single binary

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

## htop

[htop](https://hisham.hm/htop/) is a enhanced version of `top` which comes preinstalled on most systems.
- *P* &rarr; sort by CPU
- *M* &rarr; sort by memory usage
- *F4* &rarr; filter processes by string
- *space* &rarr; mark a single process

Settings are stored in `$HOME/.config/htop/htoprc` but overwritten by the application by pressing `F10` save and exit.

## mu-repo

[mu-repo](http://fabioz.github.io/mu-repo/)

- manage multiple git repos
- run git commands on multiple repos

## ngrep

[ngrep](https://github.com/jpr5/ngrep)

- user friendly `tcpdump` alternative
- written in C
- PCAP based

## prettyping

[prettyping](https://github.com/denilsonsa/prettyping)

- wrapper around ping
- written in shell
- colorful and easy to read

## ripgrep

ripgrep](https://github.com/BurntSushi/ripgrep)

- `grep` alternative
- written in Rust
- fast
- mostly grep compatible

[Comprehensive comparison](https://beyondgrep.com/feature-comparison/) of grep alternatives.

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
