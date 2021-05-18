---
title: live.jrgnsn.net
description: 
published: true
date: 2021-04-07T16:38:03.088Z
tags: needs-update
editor: markdown
dateCreated: 2021-04-07T15:38:17.071Z
---

Download nginx:

```
$ curl -LO http://nginx.org/download/nginx-1.18.0.tar.gz 
```

Download nginx-rtmp-module:

```
$ curl -LO https://github.com/sergey-dryabzhinsky/nginx-rtmp-module/archive/dev.zip
```

Extract the files and enter the nginx directory:

```
$ tar xzvf nginx-1.18.0.tar.gz
$ unzip dev.zip
$ cd nginx-1.18.0
```

Configure and make nginx:

```
$ ./configure \
--add-module=../nginx-rtmp-module-dev \
--with-http_v2_module \
--with-mail \
--with-http_dav_module \
--with-http_auth_request_module \
-- with-http_slice_module \
-- with-http_stub_status_module
$ make
$ sudo make install
```

You can test your configuration:

```
$ sudo /usr/local/nginx/sbin/nginx -t -c /etc/nginx/nginx.conf
```

## See also

[Selecting the nginx module to build](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#selecting-the-nginx-modules-to-build) (Nginx Docs)