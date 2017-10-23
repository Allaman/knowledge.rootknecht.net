---
title: 'Fix apt-get Hashsum mismatch in Debian 9'
taxonomy:
    category:
        - Others
    author:
        - Knecht
---

/etc/apt/apt.conf.d/99fixbadproxy
```
Acquire::http::Pipeline-Depth 0;
Acquire::http::No-Cache true;
Acquire::BrokenProxy    true;
```