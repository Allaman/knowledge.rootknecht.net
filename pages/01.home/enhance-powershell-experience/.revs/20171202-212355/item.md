---
title: 'Enhance Powershell Experience'
taxonomy:
    category:
        - Windows
---

## Make it more bash like

Install [PSReadLine](https://github.com/lzybkr/PSReadLine) optionally as current user if your are lacking admin rights. PSReadLine provides several features which are known from bash.

```powershell
Install-Module [-Scope CurrentUser] PSReadLine
```
Add `Import-Module PSReadLine` to C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (create file if necessary) to autoload the module upon powershell start.

Set keybinding to Emacs which allows to use common bash key combos, e.g. `ctrl+a` for jumping to the beginning of the line
```powershell
Set-PSReadlineOption -EditMode Emacs
```

Enable history search forward/backward auto completion with
```powershell
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
```