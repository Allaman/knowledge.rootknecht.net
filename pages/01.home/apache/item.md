---
title: Apache
taxonomy:
    category:
        - Applications
---

## Simple rewrite http to https
```ini
RewriteEngine On
RewriteRule ^/app1(.*)$ https://example.com/app1$1 [R,L]
RewriteRule ^/app2(.*)$ https://example.com/app2$1 [R,L]
```

## Basic authentication
```bash
sudo htpasswd -c /etc/apache2/htpasswd user1
sudo htpasswd /etc/apache2/htpasswd user2 # no -c when file exists
```
/etc/apache2/apache2.conf
```ini
<Directory "/var/www/html">
    AuthType Basic
    AuthName "NO ACCESS"
    AuthUserFile /etc/apache2/htpasswd
    Require valid-user
</Directory>
```
/var/www/html/.htaccess
```ini
AuthType Basic
AuthName "NO ACCESS"
AuthUserFile /etc/apache2/htpasswd
Require valid-user
```