---
title: DokuWiki
---

# Installing DokuWiki on Debian 9 (Stretch) or Ubuntu 18.04 (Bionic Beaver)

Installing [DokuWiki](https://www.dokuwiki.org/) is a relatively straightforward process on Debian and it's derivatives. The gist of it is: download DokuWiki, extract and copy the files to `/var/www/` or wherever you'd like, and configure your web server. I'm using [Nginx](https://nginx.org/).

A longer form of these instructions can be found at [DokuWiki's own documentation](https://www.dokuwiki.org/install).

## Downloading and Installing

Simply navigate to https://download.dokuwiki.org, customize your package and download to your server.

Extract the archive and copy it to its destination:

```
$ tar xzvf dokuwiki.tgz
$ sudo cp -r dokuwiki /var/www/
```

Give your web server user access, on Debian and its derivatives, this is usually `www-data`:

```
$ sudo chown -R www-data:www-data dokuwiki
```

## Configuring the Web Server

As stated earlier, I'm using Nginx as my web server. I create a Nginx configuration file for each domain/subdomain. I crafted my config file using [DokuWiki's example](https://www.dokuwiki.org/install:nginx).

I use [EFF's Certbot](https://certbot.eff.org/) to generate an SSL certificate from [Let's Encrypt](https://letsencrypt.org/).

## Increasing File Upload Limit

There's several places you may need to check to increase the file upload size limit from the default 2 MB.

Since I use Nginx, I had to modify the following line in my site configuration file.

`/etc/nginx/sites-available/wiki.conf`:

```nginx
client_max_body_size 26M;
```

I made it 26 MB instead of 25 MB in case I were to ever try to upload a 25 MB file, the rest of the request doesn't cause me to exceed the max.

Then I needed to change the FCGI settings for php-fpm.

`/etc/php/7.0/fpm/php.ini`:

```ini
...
post_max_size = 25M
...
upload_max_filesize = 25M
...
```

**Note:** You may need to change the `post_max_size = 25M` to `26M` if you run into issues uploading a file that's *exactly* 25MB large.


Restart nginx and php-fpm for the changes to take effect:

```
$ sudo nginx -s reload
$ sudo service php7.0-fpm restart
```

# Additional Resources

* [Maximum Upload File Size](https://www.dokuwiki.org/faq:uploadsize)

# Nginx Configuration

```nginx
server {
    listen 80;

    server_name wiki.domain.tld;

    # Maximum file upload size is 4MB - change accordingly if needed
    client_max_body_size 50M;
    client_body_buffer_size 128k;

    root /var/www/dokuwiki;
    index doku.php;

    #Remember to comment the below out when you're installing, and uncomment it when done.
    location ~ /(conf/|bin/|inc/|install.php) { deny all; }

    #Support for X-Accel-Redirect
    location ~ ^/data/ { internal ; }

    location ~ ^/lib.*\.(js|css|gif|png|ico|jpg|jpeg)$ {
        expires 365d;
    }

    location / { try_files $uri $uri/ @dokuwiki; }

    location @dokuwiki {
        # rewrites "doku.php/" out of the URLs if you set the userwrite
        # setting to .htaccess in dokuwiki config page
        rewrite ^/_media/(.*) /lib/exe/fetch.php?media=$1 last;
        rewrite ^/_detail/(.*) /lib/exe/detail.php?media=$1 last;
        rewrite ^/_export/([^/]+)/(.*) /doku.php?do=export_$1&id=$2 last;
        rewrite ^/(.*) /doku.php?id=$1&$args last;
    }

    location ~ \.php$ {
        try_files $uri $uri/ /doku.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param REDIRECT_STATUS 200;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        # fastcgi_pass unix:/var/run/php5-fpm.sock; #old php version
    }

}
```