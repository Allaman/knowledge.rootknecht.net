---
title: 'Powershell Tricks'
taxonomy:
    category:
        - Windows
    author:
        - Knecht
---

## Aliase

To create persistant aliase create the file `C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (folder might not exist).

You might have to allow the execution of powershell scripts on your system: 'Set-ExecutionPolicy -Scope CurrentUser BYPASS' (keep security policies in mind)

```powershell
function f_workspace {Set-Location "C:\Users\<user>\Documents\workspace"}
Set-Alias workspace f_workspace
function f_up {docker-compose.exe up }
Set-Alias dup f_up
function f_images {docker images}
Set-Alias di f_images
function f_ps {docker ps}
Set-Alias dps f_ps
function f_dexec {docker exec -it}
Set-Alias dexec f_dexec
```

## Grep

```powershell
Get-Content file.txt | Select-String -Pattern abcdef # Single file
Get-ChildItem -recurse | Select-String -Pattern abcdef # All files in directory
```

## Redirect all output
```powershell
 *>&1 > log.txt
```