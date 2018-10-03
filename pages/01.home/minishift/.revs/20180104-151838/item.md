---
title: Minishift
taxonomy:
    category:
        - Others
---

[TOC]

## Requirements

- HyperV (Windows 10 Enterprise, Professional, or Education)
- or VirtualBox 5.1.12 or later
- [Minishift Binary](https://github.com/minishift/minishift/releases)

## Installation

### With HyperV

1. Enable HyperV with a Powershell as administrator

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName:Microsoft-Hyper-V -All
    ```
    Reboot
    
    [More options](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

1. Add user to HyperV group

	Run powershell as administrator
	```powershell
    ([adsi]”WinNT://./Hyper-V Administrators,group”).Add(“WinNT://$env:UserDomain/$env:Username,user”)
    ```
    
1. Create virtual Switch
	See [docs.microsoft](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/connect-to-network)
 
1. Set environment variable to the name of the created virtual switch
	
    ```powershell
    set HYPERV_VIRTUAL_SWITCH=
    ```

1. Run minishift
	
    ```powershell
    minishift.exe start
    ```
 
### With Virtualbox

1. Disable HyperV if appropriate
	
    ```powershell
    Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
    ```
1. Run Minishift

    ```powershell
    minishift.exe start --vm-driver virtualbox --show-libmachine-logs --iso-url file://C:/path/to/minishift-b2d.iso
    ```
