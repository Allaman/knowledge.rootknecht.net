---
title: tmux
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

## Why

1. Multiple shell windows and panes from a single connection
2. Session functionality which survices disconnects
3. Session sharing
4. Extensible
5. Keyboard driven

## Basic concepts

1. **Windows** are like tabs in your internet browser
2. **Panes** are splits of windows each containing an individual shell
3. **Sessions** represent a state of different windows and panes

## Starting tmux

Start tmux from scratch, with a session or with a named session
```bash
tmux [ a [ -t session ] ]
```


## Basic commands

Commands are composed of the **tmux prefix (default CTRL+b) and the actual command**.

|command|action|
|-------------|---------|
| prefix c|create new window|
| prefix n|switch to window number n|
| prefix x|kill current window|
| prefix %|split window vertically|
| prefix "|split window horizontally|