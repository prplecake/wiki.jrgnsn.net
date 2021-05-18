---
title: CyTube
---

> Node.JS Server and JavaScript/HTML Client for synchronizing online media
>     - [CyTube repo](https://github.com/calzoneman/sync)

The project documentation is lacking and includes a warning saying so. If you happen across my documentation here, I hope it can be of use to you.

To get TLS working I linked the certificate and public keys from Let's Encrypt's directories.

```
sudo ln -s /etc/letsencrypt/live/cytube.splat.soy/privkey.pem /opt/cytube/privkey.pem
sudo ln -s /etc/letsencrypt/live/cytube.splat.soy/fullchain.pem /opt/cytube/fullchain.pem
```

See: [Allow Non-Root Access to Let's Encrypt Certificates](/Sysadmin/KB/Allow_Non-Root_Access_to_Let's_Encrypt_Certificates)

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