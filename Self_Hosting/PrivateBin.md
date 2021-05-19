---
title: PrivateBin
---

# nginx configuration

```nginx
server {
    listen 80;
    root /var/www/paste;

    # Add index.php to the list if you are using PHP
    index index.php index.html index.htm;

    access_log off;
    error_log off;

    server_name paste.domain.tld;

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        # try_files $uri $uri/ =404;
        try_files $uri $uri/ /index.php$is_args$args;
    }

    # pass PHP scripts to FastCGI server
    #
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;

        fastcgi_param SERVER_SOFTWARE "";
    }
}
```