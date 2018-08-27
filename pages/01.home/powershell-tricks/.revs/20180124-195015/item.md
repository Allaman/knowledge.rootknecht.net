---
title: 'Powershell Tricks'
taxonomy:
    category:
        - Windows
---

## Aliase

To create persistant aliase create the file `C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (folder might not exist).

You might have to allow the execution of powershell scripts on your system: `Set-ExecutionPolicy -Scope CurrentUser`

```powershell
function f_workspace {Set-Location "C:\Users\<user>\Documents\workspace"}
Set-Alias workspace f_workspace
```

## Grep

```powershell
Get-Content file.txt | Select-String -Pattern abcdef # Single file
Get-ChildItem -recurse | Select-String -Pattern abcdef # All files in directory
```