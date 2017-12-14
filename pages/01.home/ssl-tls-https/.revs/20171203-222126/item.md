---
title: SSL/TLS/HTTPS
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

[TOC]

## Generate self-signed certificate for https
```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```
## Remove password from protected certificate key
```bash
openssl rsa -in original.key -out unencripted.key
```
## Lets encrpyt certificate
Instead of cert.pem use fullchain.pem to prevent "missing local issuer" error

## Check a private key
```bash
openssl rsa -in priv.key -check
```

## Check a certificate
```bash
openssl x509 -in cert.pem -text -noout
```

## Check a pksc12 certificate
```bash
openssl pkcs12 -info -in keyStore.p12
```

## Convert a pksc12 certificate to pem
```bash
openssl pkcs12 -in keyStore.[pfx|p12] -out keyStore.pem -nodes
```
`-nocerts` to only output the private key or `-nokeys` to only output the certificates.