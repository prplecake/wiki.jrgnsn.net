---
title: Allow Non-Root Access to Let's Encrypt Certificates
---

This guide assumes you're using EFF's [Certbot](https://certbot.eff.org/).

> This guide may not be complete. Use extra caution, especially when setting permissions on `/etc/letsencrypt`.
{.is-warning}


First, I created a new user group for users who need access to certificates:

```
$ sudo addgroup letsencrypt
```

I added a user to that group:

```
$ sudo usermod -G letsencrypt cytube
```

Next, we need to modify permissions on /etc/letsencrypt:

```
$ sudo chmod -R 750 /etc/letsencrypt/archive
$ sudo chmod 750 /etc/letsencrypt/live
```

See also

* <https://robmclarty.com/blog/how-to-secure-your-web-app-using-https-with-letsencrypt>