---
title: Jenkins
taxonomy:
    category:
        - Applications
    author:
        - Knecht
---

## Reverse proxy config

! Adjust jenkins prefix accordingly!

```nginx
      location ^~ /jenkins/ {
        # TODO
        proxy_pass http://xxx.xxx.xxx.xxx:8080/jenkins/;
        proxy_set_header   Host             $host:$server_port;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_max_temp_file_size 0;
        client_max_body_size       10m;
        client_body_buffer_size    128k;
        proxy_connect_timeout      90;
        proxy_send_timeout         90;
        proxy_read_timeout         90;
        proxy_temp_file_write_size 64k;
        proxy_http_version 1.1;
        proxy_request_buffering off;
        proxy_buffering off;
      }
```
In case of bad proxy configuration warning in Jenkins ensure that the `Jenkins URL` in the settings ist with port number!