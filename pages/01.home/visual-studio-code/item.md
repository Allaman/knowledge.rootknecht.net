---
title: 'Visual Studio Code'
taxonomy:
    category:
        - Application
---

## Config files
Windows: `%APPDATA%\Code - Insiders\User\`

Linux: `.config/Code\ -\ Insiders`

## Syncing settings

I implemented a rather minimal but working [settings synchronization](https://repo.rootknecht.net/allaman/vsc-sync) for visual studio code as a Python CLI. It works like its "big brother" [Shan.code-settings-sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) by creating gists containing the settings.

## Manage extensions from CLI

```sh
[code | code-insiders] 
--list-extensions 
--uinstall-extension 
--uninstall-extension
```

## Recommended extensions

### Languages and frameworks
- haaaad.ansible
- evilz.vscode-reveal
- emilast.LogFileHighlighter
- joaompinto.asciidoctor-vscode
- James-Yu.latex-workshop
- lextudio.restructuredtext
- marcostazi.VS-code-vagrantfile
- ms-python.python
- ms-vscode.Go
- ms-vscode.PowerShell
- PeterJausovec.vscode-docker
- rebornix.ruby
- redhat.java
- redhat.vscode-yaml
- timonwong.shellcheck
- shd101wyy.markdown-preview-enhanced
- ms-kubernetes-tools.vscode-kubernetes-tools

### Programming helper
- **patrys.vscode-code-outline**
- **eamodio.gitlens**
- **annsk.alignment**
- plus5keen.word-counter
- ritwickdey.LiveServer
- HookyQR.beautify
- lonefy.vscode-JS-CSS-HTML-formatter
- mohsen1.prettify-json

### Tools
- **alefragnani.project-manager**
- **Molunerfinn.revealfileinfolder**
- **Shan.code-settings-sync**
- **sleistner.vscode-fileutils**
- **christian-kohler.path-intellisense**
- ban.spellright
- helixquar.randomeverything
- humao.rest-client
- RomanPeshkov.vscode-text-tables
- Tyriar.shell-launcher