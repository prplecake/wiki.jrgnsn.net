# Basics

## Logging in as root

```
sudo mysql -u root -p
```

**Note:** You can omit `-p` if you don't need a password.

## Listing all databases

```sql
SHOW DATABASES;
```

## Create User and Database

Login to database server as root:
```sh
$ sudo mysql
```

Create Database:
```sql
CREATE DATABASE database_name;
```

Create User and grant privileges:
```sql
CREATE USER 'database_user'@'localhost' IDENTIFIED BY 'user_password';
GRANT ALL PRIVILEGES ON database_name.* TO 'database_user'@'localhost';
FLUSH PRIVILEGES;
```

## Drop a database

```sql
DROP DATABASE db1;
```

# Backup and Restore

## Backup 

```sh
mysqldump --user=wikidb_user --password=wikidb_userpassword wikidb > file.sql
```
