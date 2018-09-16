---
title: Apache
taxonomy:
    category:
        - Application
        - Linux
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

## Send custom headers as reverse proxy
Some applications require to receive custom headers in order to work, e.g. Syncthing expects a X-API-KEY header in a request.

```apache
<VirtualHost *:443>
        Header add HEADER "VALUE"
        RequestHeader set HEADER "VALUE"
</VirtualHost>
```

## Enable browser cache

mod_expires

```bash
a2enmod expires
systemctl restart apache2
```

.htaccess
```ini
 <IfModule mod_expires.c>
   ExpiresActive On
   ExpiresByType application/vnd.ms-fontobject "access plus 1 year"
   ExpiresByType application/x-font-ttf "access plus 1 year"
   ExpiresByType application/x-font-opentype "access plus 1 year"
   ExpiresByType application/x-font-woff "access plus 1 year"
   ExpiresByType image/svg+xml "access plus 1 year"
   ExpiresDefault "access plus 2 days"
   ExpiresByType text/html "access plus 2 days"
   ExpiresByType image/gif "access plus 3 months"
   ExpiresByType image/jpeg "access plus 3 months"
   ExpiresByType image/jpg "access plus 3 months"
   ExpiresByType image/png "access plus 3 months"
   ExpiresByType image/x-png "access plus 3 months"
   ExpiresByType text/css "access plus 8 days" 
   ExpiresByType text/javascript "access plus 7 days"
   ExpiresByType application/x-javascript "access plus 7 days"
   ExpiresByType application/javascript "access plus 7 days"
   ExpiresByType image/x-icon "access plus 3 months"
 </IfModule>
```

mod_headers

```bash
a2enmod headers
systemctl restart apache2
```

.htaccess (or apache.conf)
```ini
<IfModule mod_headers.c>
<FilesMatch "\.(gif|ico|jpeg|jpe|png|css|js)$">
Header set Cache-Control "max-age=604800, public"
</FilesMatch>
</IfModule>
```
