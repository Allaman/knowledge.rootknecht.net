---
title: Shell
taxonomy:
    category:
        - Shell
---

[TOC]

## Auto complete a command with history-search
This setting allows you to enter shell commands quite efficient. You just enter the first couple of letters of a coomand and press page up/down. The shell tries to auto complete them based on your previous commands.

In /etc/inputrc
```bash
# alternate mappings for "page up" and "page down" to search the history
"\e[5~": history-search-backward
"\e[6~": history-search-forward
```

## Force changes to /etc/hosts
```bash
systemctl restart nscd
```

## Write multiple lines without editor

```bash
echo "line 1
line 2" >> multiple
```
or

```bash
cat <<EOT >> multiple
line 1
line 2
EOT
```

## Disable HTTPS Certificate Verification

**wget**
```bash
--no-check-certificate
```

**git**
```bash
-c http.sslVerify=false
```
or in .git/config 
```ini
[http]
sslVerify = false
```
**curl**
```bash
--insecure
```

**conda**
```bash
conda config --set ssl_verify false
```

**pip**
```bash
pip install [--index-url=http://pypi.python.org/simple/] --trusted-host pypi.python.org
```

**npm**
```bash
npm config set strict-ssl false
npm config set loglevel error
```

## Create user with predefined password
```bash
useradd -p $(openssl passwd -1 $PASS) $USER
```

## Copy permissions from existing file
```bash
chown --reference=otherfile newFile
chmod --reference=otherfile newFile
```

## Modify ownership of symlinks
```bash
chown -h USER:GROUP SYMLINK
```

## Redirect command output
**stderr and stdout**
```bash
command > /dev/null 2>&1
# bash only
command &> /dev/null
```

**only stderr**
```bash
command 2> /dev/null
```

**only stdout**
```bash
command 1> /dev/null
```

## Inherit permissions from parent directory
```bash
chmod g+s /path/to/parent
```

## Curl for REST API
**Auth**
```bash
# Auth with username password and store cookie information
curl -c cookies.txt -X POST -d 'username=admin&password=admin' https://example.com/login
# Use cookie auth information to post data from json file
curl -b cookies.txt -d @data.json -H "Content-Type: application/json" -X POST https://example.com/rest
# Use auth token
curl -H "X-Auth-Token: <Token ID>" https://example.com/login
```
**GET**
```bash
curl -H "Accept:application/json" https://httpbin.org/get
```
**POST**
```bash
curl \
-h "Content-type: application/json" \
-X POST \
-d '{"title": "Test Title", "note": "Test note"}' \
https://httpbin.org/
```

## Add existing user to group
```bash
usermod -a -G group user
```

## Reduce size of pdf files with ghostscript
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=OPTION -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```
common options for dPDFSETTINGS are:

- dPDFSETTINGS=/screen lower quality, smaller size.
- dPDFSETTINGS=/ebook for better quality, but slightly larger pdfs.
- dPDFSETTINGS=/prepress output similar to Acrobat Distiller "Prepress Optimized" setting
- dPDFSETTINGS=/printer selects output similar to the Acrobat Distiller "Print Optimized" setting
- dPDFSETTINGS=/default selects output intended to be useful across a wide variety of uses, possibly at the expense of a larger output file

## Generate hash for passwords
```bash
echo "password" | sha1sum
```

## Run multiple commands in background
```bash
(command1 &) && (command2 &)
```

## Replace whitspace with underscore in all filenames in current directory
```bash
for f in *\ *; do mv "$f" "${f// /_}"; done
```
## Shows what is in file 2 but not in file 1
```bash
grep -v -F -x -f
```
## Get SSL/TLS certificate information
```bash
alias get-ssl-cert='echo Q |openssl s_client -connect' # prints certificate
alias get-ssl-fingerprint='openssl x509 -in cert.pem -sha1 -noout -fingerprint'
```
Example:
```bash
get-ssl-cert google.com:443 > cert.pem
get-ssl-fingerprint # assumes cert.pem in current directory
```
## Merge all pdf files in current directory
```bash
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=merged.pdf *.pdf
```
## Generate handout from given pdf file
```bash
pdfjam --nup 2x3 --frame true --noautoscale false --delta "0.2cm 0.3cm" --scale 0.95
```
## Get BIOS version
```bash
sudo dmidecode | grep BIOS
```
## Get external IP
```bash
echo $(curl -ss http://ipecho.net/plain)
```
## Upgrade all pip packages
```bash
sudo pip freeze --local | grep -v '"'"'^\-e'"'"' | cut -d = -f 1  | xargs -n1 sudo pip install -U
```
## Convert all files in the directory to unix line endings

```bash
find . -type f -print0 | xargs -0 dos2unix
```

## Ommit first line of stdout

```bash
awk '{if(NR>1)print}'
```