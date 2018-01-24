---
title: 'Powershell Aliase'
taxonomy:
    category:
        - Windows
    author:
        - Knecht
---

To create persistant aliase create the file `C:\Users\<user>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` (folder might not exist).

You might have to allow the execution of powershell scripts on your system: `Set-ExecutionPolicy -Scope CurrentUser`

## Alias for changing directory:

```powershell
function f_workspace {Set-Location "C:\Users\<user>\Documents\workspace"}
Set-Alias workspace f_workspace
```