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