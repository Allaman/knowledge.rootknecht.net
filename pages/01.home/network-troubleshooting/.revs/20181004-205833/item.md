---
title: 'Network Troubleshooting'
taxonomy:
    category:
        - Linux
---

[TOC]

## Check DNS

Check alos `dnsmasq` and `/etc/resolv.conf`

### nslookup
```bash
nslookup DOMAIN.TLD # A record
nslookup IP # rDNS
nslookup -query=any DOMAIN.TLD # query all DNS records
```

### dig
```bash
dig DOMAIN.tld [+short]
dig -x IP +short # rDNS
dig DOMAIN.tld TTL # TTL record
dig DOMAIN.tld ANY +noall +answer # query all DNS records
```

## Check Traceroute
```bash
traceroute www.google.com # uses UDP data on random port
traceroute -I www.google.com # uses ICMP data
traceroute -T -p 80 www.google.com # fix TCP port to test path to services to bypass firewalls
mtr -rw www.google.com #send 10 packets and generate report
```

## Check DHCP traffic
```bash
dhcpdump -i INTERFACE
# udp 67 server, udp 68 client
tcpdump -i INTERFACE port 67 or port 68 -e -n
```

## Check bandwidth

### iperf

On your server start
```bash
iperf -s -p SERVERPORT
```
On your client
```bash
iperf -c SERVERIP -p SERVERPORT -t 15 -i 1 -f m
```
- -t 15 runs for 15 secons
- -l 1 shows output every second
- -f m shows rate in Mbps

## Check open ports
local
```bash
lsof -i -P -n [ | grep LISTEN]
ss -tan
netstat -tulpen
```
on remote
```bash
telnet HOST PORT
nc -zv HOST PORT[-][PORT]
nmap -source-port PORT HOST
```

programmatically
```bash
#!/bin/bash
ip=$1
ports=( 5443 3443 6443 8443 7443 22 23 7079 8079 80 8080 )
for port in "${ports[@]}"
do
  nc -z -v -w5 $ip $port
done
```

## Check traffic on interface
```bash
iftop -i INTERFACE
nethogs device INTERFACE
```

## Routes
List routes
```bash
ip route
route -n
```
Add default gateway
```bash
ip route add default via GATEWAYIP
route add default gw GATEWAYIP
```

## Scan with nmap

```bash
nmap -p 1-100 # scan ports
nmap -p- # scan all ports
nmap -sT # use  TCP connect
nmap -sS # use TCP SYN
nmap -sU # scan UDP
nmap -A # OS and service detection
nmap -sV [--version-intensity 5] # Standard service detection (increased agressivity
nmap -oX outputfile.xml # save as XML
nmap -oG outputfile.txt # save for grep

```

Analyze nmap output with [NetworkScanViewer](http://www.woanware.co.uk/network/networkscanviewer.html)