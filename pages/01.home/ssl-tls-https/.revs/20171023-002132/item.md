---
title: SSL/TLS/HTTPS
taxonomy:
    category:
        - Shell
---

## Generate self-signed certificate for https
```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```
## Remove password from protected certificate key
```bash
openssl rsa -in original.key -out unencripted.key
```