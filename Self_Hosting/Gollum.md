---
title: Gollum
---

[Gollum](https://github.com/gollum/gollum) is "a simple, Git-powered
wiki with a sweet API and local frontend."

## Install

Installing on Debian/Ubuntu

```
$ sudo apt update; sudo apt upgrade
$ sudo apt install rubygems ruby-dev make cmake libssl-dev
$ sudo gem install gollum
```

## Prep the remote repository

```
$ sudo mkdir -p /path/to/wiki
$ sudo chown -R git:git /path/to/wiki
$ sudo -Hu git git init --bare
```

## Systemd Service

```
[Unit]
Description=Gollum, a simple git-powered wiki
After=network.target

[Service]
User=git
ExecStart=/usr/local/bin/gollum --no-edit "/path/to/wiki"
```

## Nginx Configuration

```nginx
server {
	
	listen 80;
	server_name wiki.example.com;

	access_log /var/log/nginx/wiki/access.log;
	error_log /var/log/nginx/wiki/error.log;

	location / {
		proxy_pass http://127.0.0.1:4567;
	}
}
```