---
title: 'Shell Aliases'
taxonomy:
    category:
        - Shell
    author:
        - Knecht
visible: false
---

[TOC]
## Replace whitspace with underscore in all filenames in current directory
```bash
alias replace_ws_with_underscore='for f in *\ *; do mv "$f" "${f// /_}"; done'
```
## Shows what is in file 2 but not in file 1
```bash
alias filediff='grep -v -F -x -f'
```
## Get SSL/TLS certificate information
```bash
alias get-ssl-cert='echo Q |openssl s_client -connect'
alias get-ssl-fingerprint='openssl x509 -in cert.pem -sha1 -noout -fingerprint'
```
Example:
```bash
get-ssl-cert google.com:443 > cert.pem
get-ssl-fingerprint # assumes cert.pem in current directory
```
## Merge all pdf files in current directory
```bash
alias pdfmerge='gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=merged.pdf *.pdf'
```
## Generate handout from given pdf file
```bash
alias genhandout='pdfjam --nup 2x3 --frame true --noautoscale false --delta "0.2cm 0.3cm" --scale 0.95'
```
## Get BIOS version
```bash
alias biosversion='sudo dmidecode | grep BIOS'
```
## Get external IP
```bash
alias externalip='echo $(curl -ss http://ipecho.net/plain)'
```
## Upgrade all pip packages
```bash
alias pipupgrade='sudo pip freeze --local | grep -v '"'"'^\-e'"'"' | cut -d = -f 1  | xargs -n1 sudo pip install -U'
```
## Convert all files in the directory to unix line endings
```bash
alias dos2unix-folder='find . -type f -print0 | xargs -0 dos2unix'
```