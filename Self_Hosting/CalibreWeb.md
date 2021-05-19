# nginx config
```nginx
server {
    listen 80;
    server_name calibre.example.com;

    client_max_body_size 1G;

    location / {
        proxy_bind          $server_addr;
        proxy_pass          http://127.0.0.1:8083;
        proxy_set_header    Host            $http_host;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    X-Scheme        $scheme;
    }

}
```

# systemd service

```
[Unit]
Description=calibre-web

[Service]
Type=simple
User=calibre
Group=calibre
ExecStart=/usr/bin/python3 /home/calibre/calibre-web/cps.py
WorkingDirectory=/home/calibre/calibre-web

[Install]
WantedBy=multi-user.target
```

# See also
* <https://github.com/janeczku/calibre-web>