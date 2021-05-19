---
title: Ghost blog
---

# Systemd Service

This is a service that runs the [Ghost](https://ghost.org/) blogging platform on boot. Also provides `start`, `stop`, `restart`, and `status` commands. 

```
[Unit]
Description=ghost
After=network.target

[Service]
Type=simple
# Edit WorkingDirectory, User and Group as needed
WorkingDirectory=/home/ghost/ghost
User=ghost
Group=ghost
ExecStart=/usr/bin/npm start --production
ExecStop=/usr/bin/npm stop --production
Restart=always
SyslogIdentifier=Ghost

[Install]
WantedBy=multi-user.target
```