---
title: 'Network Troubleshooting'
---

## Chech DNS
```bash

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
```bash
lsof -i :PORT
ss -tan
netstat -tulpen
```