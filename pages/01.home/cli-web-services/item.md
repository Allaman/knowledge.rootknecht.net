---
title: 'CLI Web Services'
taxonomy:
    category:
        - Application
---

## Weather

```sh
curl wttr.in/München
```
  
## Crypto currencies

```sh
curl eur.rate.sx/eth
```

## External IP

```sh
curl ipecho.net/plain
```

## Translator

Translates marked text with the Google translate API and displays the result via `notify-send`

```sh
notify-send --icon=info "$(xsel -o)" "$(wget -U "Mozilla/5.0" -qO - "http://translate.googleapis.com/translate_a/single?client=gtx&sl=auto&tl=de&dt=t&q=$(xsel -o | sed "s/[\"'<>]//g")" | sed "s/,,,0]],,.*//g" | awk -F'"' '{print $2, $6}')"
```

## Cheatsheet

```sh
curl cht.sh/ls
curl cht.sh/python/dirs+recursive
```
See [cheat.sh](https://knowledge.rootknecht.net/cli-applications#cheat-sh)
    
## Latencies

```sh
curl cheat.sh/latencies
```
  
## Generate QR codes

```sh
curl qrenco.de/https://google.com
curl qrenco.de/Hello%20World
```
  
## URL Shortener

```sh
curl -s http://tinyurl.com/api-create.php\?url=https://google.com
```
    
## Random commit messages

```sh
curl -sk https://whatthecommit.com/index.txt
```
  
## Star Wars in terminal

```sh
nc towel.blinkenlights.nl 23
```
