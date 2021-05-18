---
title: FreshRSS
---

[FreshRSS](https://www.freshrss.org/) is an easy to use, simple, self-hostable feed aggregator. The iOS app [Reeder](https://www.reederapp.com/) is my preferred RSS app on my phone, and supports FreshRSS.

## nginx configuration

> To use this configuration, you’ll need to create the directory `/var/log/nginx/freshrss`.
{.is-warning}

```nginx
server {
    listen 80;
    server_name feeds.domain.tld;

    root /var/www/freshrss/p/;

    index index.php index.html index.htm;

    access_log /var/log/nginx/freshrss/access.log;
    error_log /var/log/nginx/freshrss/error.log;

    location ~ ^.+?\.php(/.*)?$ {
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location / {
        try_files $uri $uri/ index.php;
    }
}
```