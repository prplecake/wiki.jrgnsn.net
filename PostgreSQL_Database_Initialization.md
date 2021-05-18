---
title: PostgreSQL Database Initialization
description: 
published: true
date: 2021-04-07T17:40:24.456Z
tags: postgresql
editor: markdown
dateCreated: 2021-04-07T17:40:18.838Z
---

# Tl;dr

```
sudo -u postgres psql
postgres=# create database mydb;
postgres=# create user myuser with encrypted password 'mypass';
postgres=# grant all privileges on database mydb to myuser;
```

# See also

* [Creating user, database and adding access on PostgreSQL](https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e)