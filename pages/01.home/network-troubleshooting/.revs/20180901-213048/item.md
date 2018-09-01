---
title: 'Network Troubleshooting'
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
lsof -i :PORT
ss -tan
netstat -tulpen
```
on remote
```bash
telnet HOST PORT
nc -zv HOST PORT[-][PORT]
nmap -source-port PORT HOST
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
