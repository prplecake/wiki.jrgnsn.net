---
title: Nextcloud
---

# Local Caching[^1]

```
$ sudo apt install php-acpu
$ sudo service php7.2-fpm restart
```

# Run Background Jobs[^2]

Edit www-data user's crontab:

```
$ sudo -Hu www-data crontab -e
```

Add this line:

```
*/5 * * * * php -f /var/www/nextcloud/cron.php
```

# See also

* [/nginx config](/Self_Hosting/Nextcloud/Nginx_config)


# References

[^1]:https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/caching_configuration.html?highlight=caching#id1
[^2]:https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/background_jobs_configuration.html?highlight=background%20jobs#background-jobs