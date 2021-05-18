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

> I made it 26 MB instead of 25 MB in case I were to ever try to upload a 25 MB file, the rest of the request doesn't cause me to exceed the max.
{.is-info}

Then I needed to change the FCGI settings for php-fpm.

`/etc/php/7.0/fpm/php.ini`:

```ini
...
post_max_size = 25M
...
upload_max_filesize = 25M
...
```

> **Note:** You may need to change the `post_max_size = 25M` to `26M` if you run into issues uploading a file that's *exactly* 25MB large.
{.is-info}


Restart nginx and php-fpm for the changes to take effect:

```
$ sudo nginx -s reload
$ sudo service php7.0-fpm restart
```

# Additional Resources

* [Maximum Upload File Size](https://www.dokuwiki.org/faq:uploadsize)

# See also

* [/nginx config](/Self_Hosting/DokuWiki/Nginx_config)