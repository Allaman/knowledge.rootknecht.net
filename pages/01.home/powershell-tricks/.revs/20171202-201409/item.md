---
title: 'Powershell Aliase'
taxonomy:
    category:
        - Windows
---

To create persistant aliase create the file `C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (folder might not exist).

You might have to allow the execution of powershell scripts on your system: `Set-ExecutionPolicy -Scope CurrentUser`

## Alias for changing directory:

```powershell
function f_workspace {Set-Location "C:\Users\<user>\Documents\workspace"}
Set-Alias workspace f_workspace
```

## Enhance experience with bash like experience

Install [PSReadLine](https://github.com/lzybkr/PSReadLine) optionally as current user if your are lacking admin rights:

```powershell
Install-Module [-Scope CurrentUser] PSReadLine
```

Set keybinding to Emacs which allows to use common bash key combos, e.g. `ctrl+a` for jumping to the beginning of the line
```powershell
Set-PSReadlineOption -EditMode Emacs
```