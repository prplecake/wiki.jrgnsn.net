---
title: Mastodon
description: 
published: true
date: 2021-04-07T17:37:23.683Z
tags: mastodon, fediverse
editor: markdown
dateCreated: 2021-04-07T17:36:13.428Z
---

# PgHero Issues

Lately I ran into some trouble making PgHero happy on my Mastodon server.

Here's the steps that finally worked for me.

## Problem

When checking PgHero, a nice yellow warning message reads:

> Query stats must be enabled for slow queries

## Solution

I was following this guide: https://github.com/ankane/pghero/blob/master/guides/Query-Stats.md

### Query Stats

I couldn't enable query stats from the dashboard, I had to do it manually.

Add the following to your `postgresql.conf`, I found mine at `/etc/postgresql/posgresql.conf`:

```
shared_preload_libraries = 'pg_stat_statements'
pg_stat_statements.track = all
pg_stat_statements.max = 10000
track_activity_query_size = 2048
```

Restart PostgreSQL:

```
sudo systemctl restart postgresql
```

Now we need to create the extension, but we need to do it in the right database...

1. Log into the psql console as a superuser:
    ```
    sudo -u postgres psql
    ```

2. Find and connect to your mastodon database:[^1]
    ```
    postgres=# \l
                                           List of databases
            Name         |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
    ---------------------+----------+----------+-------------+-------------+-----------------------
     mastodon_production | mastodon | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
    ...

    postgres=# \c mastodon_production
    You are now connected to database "mastodon_production" as user "postgres".
    ```

3. Now we can create the extension.
    ```
    mastodon_production=# CREATE EXTENSION pg_stat_statements;
    CREATE EXTENSION
    ```
4. That's it! PgHero should be happy now. Quit psql with `\q`.

# Uninstallation Notes

Basically the reverse of https://docs.joinmastodon.org/administration/installation/.

1. Remove Mastodon dependencies[^2]:
    ```
    $ sudo apt remove fail2ban elasticsearch redis-server redis-tools
    ```
    
2. Remove mastodon user and home directory[^3]:
    ```
    $ sudo userdel mastodon; sudo rm -rf /home/mastodon
    ```
    
3. Dump and unload mastodon database[^4]:
    ```
    $ sudo -Hu postgres pg_dump -d mastodon_production -format-custom -f /tmp/mastodon_production.pgdump
    $ sudo -Hu postgres psql
    postgres=# DROP DATABASE mastodon_production;
    postgres=# DROP ROLE mastodon;
    ```
    
4. Stop and remove mastodon systemd services:
    ```
    $ sudo systemctl stop mastodon-web.service
    $ sudo systemctl stop mastodon-sidekiq.service
    $ sudo systemctl stop mastodon-streaming.service
    $ sudo systemctl disable mastodon-web.service
    $ sudo systemctl disable mastodon-sidekiq.service
    $ sudo systemctl disable mastodon-streaming.service
    ```

[^1]:postgres=# is the prompt on my system.
[^2]:fail2ban and elasticsearch (if installed), redis-server
[^3]:can free up almost 2 GB worth of space!
[^4]:see [here](/PostgreSQL_Database_Backup_and_Restore) for postgresql backup/restore commands