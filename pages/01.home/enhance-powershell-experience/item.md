---
title: 'Enhance Powershell Experience'
taxonomy:
    category:
        - Application
---

## Make it more bash like

Install [PSReadLine](https://github.com/lzybkr/PSReadLine) (optionally as current user if your are lacking admin rights). PSReadLine provides several features which are known from bash like a history search, undo/redo, and more.

```powershell
Install-Module [-Scope CurrentUser] PSReadLine
```
Add `Import-Module PSReadLine` to C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (create file if necessary) to autoload the module upon powershell start.

Set keybinding to Emacs to use common bash key combos, e.g. `ctrl+a` for jumping to the beginning of the line
```powershell
Set-PSReadlineOption -EditMode Emacs
```

Enable history search forward/backward auto completion with
```powershell
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
```

## More extensions

* [posh-git](https://github.com/dahlbyk/posh-git) for Powershell Git integration: Install-Module posh-git `Import-Module posh-git`to your Powershell Profile
* [posh-docker](https://github.com/samneirinck/posh-docker) for Docker completion: Install-Module posh-docker and add `Import-Module posh-docker` to your Powershell Profile

## Aliase

To create persistant aliase create the file `C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (folder might not exist).

You might have to allow the execution of powershell scripts on your system: `Set-ExecutionPolicy -Scope CurrentUser BYPASS`
! keep security policies in mind

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
