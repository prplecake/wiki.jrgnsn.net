---
title: Request Tracker
description: 
published: true
date: 2021-04-07T17:43:16.417Z
tags: nginx, request-tracker, rt, rtir
editor: markdown
dateCreated: 2021-04-07T17:43:11.061Z
---

# Removing RTIR

You can simply disable the RTIR functionality by removing the plugin live from your `RT_SiteConfig.pm`. The line to be removed is:

```perl
Plugin('RT::IR');
```

# Nginx config

> To use this configuration, you’ll have to create the directory `/var/log/nginx/rt`.
{.is-warning}


```nginx
server {
	listen 80;
	server_name rt.domain.tld;
	access_log /var/log/nginx/rt/access.log;
	error_log /var/log/nginx/rt/error.log;

	location / {
		uwsgi_pass unix:///var/tmp/uwsgi.sock;
		include uwsgi_params;
		uwsgi_modifier1 5;
	}
}
```