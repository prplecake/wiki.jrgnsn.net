---
title: Config files
description: 
published: true
date: 2021-04-07T16:38:31.513Z
tags: nginx, systemd
editor: markdown
dateCreated: 2021-04-07T15:47:47.907Z
---

## nginx

This is a trimmed config, I'll leave the TLS configuration up to you.

```nginx
server {
    listen 80;
    server_name cytube.domain.tld;
    
    location ~ .* {
        proxy_pass http://localhost:8678;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_host;
    }
}
```

## systemd

`/etc/systemd/system/cytube.service`:

```
[Unit]
Description=CyTube - Online Media Synchronization Service
After=network.target

[Service]
User=cytube
WorkingDirectory=/opt/cytube
ExecStart=node index.js
ExecReload=/bin/kill $MAINPID
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

To use it:

```
$ sudo systemctl enable cytube
$ sudo systemctl start cytube
```