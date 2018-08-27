---
title: 'Unban IP from fail2ban'
taxonomy:
    category:
        - Others
---

Unban a IP blocked from fail2ban.

## Check if IP is really banned
```bash
iptables -L -n | grep IP
```

## Look for the approriate rule name
```bash
iptables -L -n
```

## Get fail2ban jail list
```bash
fail2ban-client status
```

## Unban IP
```bash
fail2ban-client set JAILNAME unbanip IP
```


