---
title: 'Network Troubleshooting'
---

## Check DHCP traffic
```bash
dhcpdump -i INTERFACE
# udp 67 server, udp 68 client
tcpdump -i INTERFACE port 67 or port 68 -e -n
```

## Check bandwidth

## Check open ports
```bash
lsof -i :PORT
ss -tan
netstat -tulpen
```