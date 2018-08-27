---
title: SSL/TLS/HTTPS
taxonomy:
    category:
        - Shell
---

[TOC]

## Generate self-signed certificate for https
**Simple usecase**
```bash
openssl req -x509 -newkey rsa:4096 -sha256 -keyout key.pem -out cert.pem -days 365
```

**Advanced usecase**
Including *S*ubject *A*lternative *N*ames
```bash
openssl req \
-newkey rsa:4096 \
-x509 \
-nodes \
-keyout key.pem \
-out cert.pem \
-subj "/C=DE/ST=Munich/L=Bavaria/O=department/OU=company/CN=example.com" \
-reqexts SAN \
-extensions SAN \
-config <(cat /etc/ssl/openssl.cnf \
    <(printf '[SAN]\nsubjectAltName=IP:127.0.0.1,DNS:localhost')) \
-sha256 \
-days 365
```
! Path of `/etc/ssl/openssl.cnf` might differ

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

## Emulate SSL/TLS Handshake
```bash
openssl s_client -state -nbio -connect HOST:PORT
```