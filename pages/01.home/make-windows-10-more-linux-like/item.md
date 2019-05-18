---
title: 'Make Windows 10 more Linux like'
taxonomy:
    category:
        - Linux
---

! Under construction!

[TOC]

## Motivation

I am a Linux[^1] user for over a decade and my workflow and productivity is optimized to this environment especially the shell[^2]. For some insights of my workflow and tools have a look at [here](https://knowledge.rootknecht.net/linux-productivity). From time to time my work demands from me to work on a Windows machine despite the fact that in my kind of business, Infrastructure and DevOps, the majority of systems and tools is Linux driven.

Now the question is how to get the best Linux like experience on a Windows 10[^3] machine specifically how to get the best shell experience and the tools that I am used to.

I want to describe some Windows tweaks and software and three ways of getting a more Linux like experience on your Windows 10 machine:

1. A combination of a virtual machine running Linux and a local SSH client
2. The Windows Subsystem for Linux basically a compatibility layer for running linux binaries (ELF)
3. Tweak and enhance the Powershell

## Built-in Windows


## Software

Generally speaking, I always prefer cross platform software to be able to have a as much as possible unified user experience across different platforms. That said have a look at my [CLI Applications](https://knowledge.rootknecht.net/cli-applications) and [GUI Applications](https://knowledge.rootknecht.net/gui-applications) summaries. Particularly, most of the GUI applications I am running are cross platform capable. Nevertheless, find some usefull Windows applications that are not necessary useful or available on Linux systems:

- [ConEmu](https://conemu.github.io/) - An enhanced terminal featuring tabs, Guake drop down style, various differents shells and much customazation options
- [MobaXterm](https://mobaxterm.mobatek.net/) - A fully featured SSH, FTP, RDP and more client with session management, tunneling, its own shell and more
- [Autohotkey](https://www.autohotkey.com/) - An open source Windows scripting tool for automation and key binding settings



## VM + SSH Client

Requirements:

- A hypervisor installed. I prefer [VirtualBox](https://www.virtualbox.org/)
- A ssh client. I prefer [MobaXterm](https://mobaxterm.mobatek.net/) but [Putty](https://www.putty.org/) will get the job done as well

|Pros|Cons|
|-------|-------|

## WSL

Requirements:

- [Enable/Install WSL](https://docs.microsoft.com/de-de/windows/wsl/install-win10)
- Choose and install a Linux distribution from. As of now the choice is Ubuntu, OpenSUSE, SLES, Kali Linux, or Debian GNU/Linux. I prefer Ubuntu for the easiest usage

|Pros|Cons|
|-------|-------|

## Powershell

Requirements:

- Powershell 4+

|Pros|Cons|
|-------|-------|

[^1]: Linux is refered to as an Linux based operationg system like Ubuntu, Arch, Debian
[^2]: or CLI, konsole, terminal, you name it 
[^3]: WSL is only available on Windows 10 64bit systems