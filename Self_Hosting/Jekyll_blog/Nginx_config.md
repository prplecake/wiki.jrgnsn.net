---
title: Nginx config
---

```nginx
server {
    listen 80;
    root /var/www/jrgnsn.net;

    # Add index.php to the list if you are using PHP
    index index.html index.htm;

    access_log /var/log/nginx/jrgnsn.net/access.log;
    error_log /var/log/nginx/jrgnsn.net/error.log;

    server_name jrgnsn.net;

    error_page 404 /404.html;
    error_page 403 /403.html;

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ /404.html;
    }

    location ~* .(css|jpg|png|gif|jpeg|js)$
    {
        access_log off;
        gzip_static on;
        gzip_comp_level 5;
        expires 1M;
        add_header Cache-Control private;
    }
}
```