---
title: 'CLI Applications'
taxonomy:
    category:
        - Application
---

A brief overview of **c**ommand **l**ine **i**nterface applications I use and higly recommend!

[TOC]

## bat

[bat](https://github.com/sharkdp/bat)

- `cat` alternative
- written in Rust
- syntax highlightning
- Git integration
- automatic paging

## cheat.sh

[cheat.sh](https://github.com/chubin/cheat.sh)

- cheatsheet interface
- written in Python
- 56 programming languages, several DBMSes, and more than 1000 UNIX/Linux commands
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

- alternative for `git diff`
- customizable and nice looking
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

See [here](https://knowledge.rootknecht.net/fzf) for some of my tweaks

## fasd

[fasd](https://github.com/clvv/fasd)

- fast navigation in your shell
- written in shell
- quickaccess to files, directories
- inspired by autojump, z, and v

## hledger

[hledger](https://hledger.org/)

- double entry accounting
- written in Haskell
- ledger compatible
- Web UI, ncurses, API, reports, and more

## htop

[htop](https://hisham.hm/htop/) is a enhanced version of `top` which comes preinstalled on most systems.
- *P* &rarr; sort by CPU
- *M* &rarr; sort by memory usage
- *F4* &rarr; filter processes by string
- *space* &rarr; mark a single process

Settings are stored in `$HOME/.config/htop/htoprc` but overwritten by the application by pressing `F10` save and exit.

## iftop

[iftop](http://www.ex-parrot.com/pdw/iftop/)

- top like interface for bandwidth usage
- written in C

## iotop

[iotop](http://guichaz.free.fr/iotop/)

- top like interface for ingoing/outgoing
- written in python

## isync

[isync](http://isync.sourceforge.net/)

- IMAP and MailDir synchronization
- written in C
- Control every aspect of synchronization

## khard

[khard](https://github.com/scheibler/khard)

- CardDAV client
- written in Python
- mutt integration
- in combination with [vdirsyncer](#vdirsyncer)

## khal

[khal](https://github.com/pimutils/khal)

- calendar application
- written in Python
- reads and writes events/icalendars
- in combination with [vdirsyncer](#vdirsyncer)

## mpv

[mpv](https://mpv.io/)

- media player
- written in C
- CLI optimized
- plays (youtube) streams

## mstmp

[msmtp](https://marlam.de/msmtp/)

- SMTP Client
- written in C
- sendmail compatible

## mu-repo

[mu-repo](http://fabioz.github.io/mu-repo/)

- manage multiple git repos
- run git commands on multiple repos
- discover git repos in your file system

## mutt

[mutt](http://www.mutt.org/)

- full featured mail client
- written in C
- highly customizable and scriptable
- vim like keybindings

## ncdu

[ncdu](https://dev.yorhel.nl/ncdu)

- ncurses disk usage
- written in C
- fast and simple to use

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

## ranger

[ranger](https://github.com/ranger/ranger)

- file manager
- written in Python
- three pane or two pane style
- highly customizable and scriptable
- vim like keybindings
- alternatives: [vifm](https://vifm.info/), [nnn](https://github.com/jarun/nnn), [mc](https://midnight-commander.org/)

## ripgrep

[ripgrep](https://github.com/BurntSushi/ripgrep)

- `grep` alternative
- written in Rust
- fast
- mostly grep compatible
- sane default settings

[Comprehensive comparison](https://beyondgrep.com/feature-comparison/) of grep alternatives.

## spacemace

[spacemacs](https://github.com/syl20bnr/spacemacs)

- Emacs distribution
- combines Emacs and Vim
- written in elisp

## spacevim

- Vim distribution
- like spacemacs for Vim
- written in Vim script

## storm

[storm](https://github.com/emre/storm)

- ssh management wrapper
- written in Python
- add, edit, delete, and list your `.ssh/config` entries
- various UIs

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

## tmux

[tmux](https://github.com/tmux/tmux)

- terminal multiplexer
- alternative to `screen`
- written in C
- [basic intro](https://knowledge.rootknecht.net/tmux)

## trash-cli

[trash-cli](https://github.com/andreafrancia/trash-cli)

- `rm` alternative respecting the trashcan
- deleted files can be restored
- written in Python

## urlview

[urlview](https://github.com/sigpipe/urlview)

- extract URLs from text
- written in C
- extract urls from mails (mutt) and more

## vdirsyncer

[vdirsyncer](https://github.com/pimutils/vdirsyncer)

- synchronize calendars and contacts
- written in Python
- CardDAV / CalDAV support
- fine control

## w3m

[w3m](http://w3m.sourceforge.net/)

- text-based web browser
- written in C
- Vim like keybindings
- renders html for other apps (like mutt)
- alternatives: [links2](http://links.twibright.com/), [Lynx](https://lynx.browser.org/), [Elinks](http://elinks.or.cz/index.html)

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

## youtube-dl

[youtube-dl](https://ytdl-org.github.io/youtube-dl/index.html)

- download videos from video platforms
- written in Python
- by far not limited to youtube
- convert videos to mp4
