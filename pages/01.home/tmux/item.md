---
title: tmux
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

## Why tmux

1. Multiple shell windows and panes from a single connection
2. Session functionality which survices disconnects
3. Session sharing
4. Extensible
5. Keyboard driven

Alternative: `screen` which comes preinstalled on most distributions

## Basic concepts

1. **Windows** are like tabs in your internet browser
2. **Panes** are splits of windows each containing an individual shell
3. **Sessions** represent a state of different windows and panes

## Starting tmux

```bash
tmux # start fresh session
tmux new-session -s NAME # create new session with NAME
tmux a # attach to session
tmux a -t NAME # attach to named session
tmux ls # list running sessions
tmux kill-session -t NAME # kill session NAME
```


## Commands

Commands are composed of the **tmux prefix (default CTRL+b) and the actual command**.

|command|action|
|-------------|---------|
| prefix c|create new window|
| prefix n|switch to window number n|
| prefix &|kill current window|
| prefix w|list windows|
| prefix ,|rename window|
| prefix .|move window to given number|
| prefix %|split window vertically|
| prefix "|split window horizontally|
| prefix x|kill current pane|
|prefix d|detach tmux (back to normal shell)|
| prefix ?|list shortcuts|
| prefix t|show big clock|

## Command prompt

With `:`you can start a command prompt similar to Vim's ex mode. Tab-autocompletion is available