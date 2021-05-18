---
title: PostgreSQL Database Backup and Restore
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