---
title: 'Shell Tricks'
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

## Auto complete a command with history-search
This setting allows you to enter shell commands quite efficient. You just enter the first couple of letters of a coomand and press page up/down. The shell tries to auto complete them based on your previous commands.

In /etc/inputrc
```bash
# alternate mappings for "page up" and "page down" to search the history
"\e[5~": history-search-backward
"\e[6~": history-search-forward
```