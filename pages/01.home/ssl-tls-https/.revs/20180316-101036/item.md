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

## Java key store vs trust store

1. trustStore is used by `TrustManager` class and keyStore is used by `KeyManager` class
1. `TrustManager` determines whether remote connection should be trusted or not; `KeyManager` decides which authentication credentials should be sent to the remote host for authentication during SSL handshake
1. `KeyStore` contains private keys and is required only if you are running a Server in SSL connection or you have enabled client authentication on server side. TrustStore stores public key or certificates from CAs which tells Java to trust a remote party or SSL connection

## Create java trust store
```bash
# Repeat for each certificate
keytool -import -file /PATH/TO/FIRSTCA.cert -alias firstCA -keystore /PATH/TO/TRUSTSTORE
```

## Use Java key / trust store
```bash
-Djavax.net.ssl.trustStore /PATH/TO/TRUSTSTORE
-Djavax.net.ssl.trustStorePassword PASSWORD
-Djavax.net.ssl.keyStore /PATH/TO/KEYSTORE
-Djavax.net.ssl.keyStorePassword PASSWORD
```

## Check HTTPS connection with Java

```java
// SSLPoke.java
import javax.net.ssl.SSLSocket;
import javax.net.ssl.SSLSocketFactory;
import java.io.*;

public class SSLPoke {
    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("Usage: "+SSLPoke.class.getName()+" <host> <port>");
            System.exit(1);
        }
        try {
            SSLSocketFactory sslsocketfactory = (SSLSocketFactory) SSLSocketFactory.getDefault();
            SSLSocket sslsocket = (SSLSocket) sslsocketfactory.createSocket(args[0], Integer.parseInt(args[1]));

            InputStream in = sslsocket.getInputStream();
            OutputStream out = sslsocket.getOutputStream();

            // Write a test byte to get a reaction :)
            out.write(1);

            while (in.available() > 0) {
                System.out.print(in.read());
            }
            System.out.println("Successfully connected");

        } catch (Exception exception) {
            exception.printStackTrace();
        }
    }
}
```
```bash
javac SSLPoke.java
java SSLPoke HOST PORT
```