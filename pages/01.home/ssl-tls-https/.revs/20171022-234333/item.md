---
title: SSL/TLS/HTTPS
---

## Generate self-signed certificate for https
```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```