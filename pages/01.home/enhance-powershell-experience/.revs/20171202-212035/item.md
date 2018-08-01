---
title: 'Enhance Powershell Experience'
---

## Make it more bash like

Install [PSReadLine](https://github.com/lzybkr/PSReadLine) optionally as current user if your are lacking admin rights. PSReadLine provides several features which are known from bash.

```powershell
Install-Module [-Scope CurrentUser] PSReadLine
```

Set keybinding to Emacs which allows to use common bash key combos, e.g. `ctrl+a` for jumping to the beginning of the line
```powershell
Set-PSReadlineOption -EditMode Emacs
```