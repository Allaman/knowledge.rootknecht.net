---
title: Windows
taxonomy:
    category:
        - Windows
---

[TOC]

## Programmatically (un)set environment variables in Winodws

Use setx in a batch file.

```batch
setx NAME "value"
```

Unset (persistant) only in the registry (execute 'regedit')
```
HKEY_CURRENT_USER\Environment
```

## Add route to reach a container in Docker for Windows

	```powershell
    route add 172.17.0.0 mask 255.255.0.0 10.0.75.2-p
    ```

- First IP address is the default Docker subnet
- The last IP address is the address of the Docker host
- The -p flag persists the change across reboots

## Autostart virtualbox manage at boot

Create a link in your autostart folder with target `"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" startvm "VM_NAME" --type headless`