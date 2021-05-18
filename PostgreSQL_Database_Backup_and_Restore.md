---
title: PostgreSQL Database Backup and Restore
description: 
published: true
date: 2021-04-07T17:37:20.781Z
tags: postgresql
editor: markdown
dateCreated: 2021-04-07T17:37:14.149Z
---

# Backup

Use `pg_dump` to backup the database:

```
$ sudo -Hu postgres pg_dump -d <database_name> -format-custom -f </path/to/backup/database.pgdump>
```

# Restore

Use `pg_restore` to load the database back up:

```
$ sudo -Hu postgres pg_restore -d <database_name> -v -1 </path/to/backup/database.pgdump>
```