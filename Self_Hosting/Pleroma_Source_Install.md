---
title: Pleroma Source Install
---

I've decided to start using [Pleroma](https://pleroma.social/) instead of [Mastodon](https://joinmastodon.org/), specifically for the lighter footprint. It was after reading [this article](https://blog.soykaf.com/post/what-is-pleroma/) that I made my decision. 

# Notes

I'm using Pleroma's guide to help me through the process:
* <https://docs-develop.pleroma.social/debian_based_en.html>

Setup was pretty straightforward. Though I ran into some issues with the database, so I needed to clean that up. The only "gotcha" I ran into was: I installed Pleroma on the same server Mastodon was running on previously. Mastodon was also running on port 4000, which was causing issues.

```
$ sudo -Hu postgres psql
postgres=# drop database pleroma;
postgres=# drop role pleroma;
```

I also made sure to turn off public registration, in `prod.secrets.exs`:

```elixir
config :pleroma, :instance,
    ...
    registrations_open: false,
    ...
```

I then went through Pleroma's own security hardening guide: <https://docs-develop.pleroma.social/hardening.html>.

# Backup/Restore your instance

## Backup

1. Stop the Pleroma service.
2. Go to the working directory of Pleroma (default is `/opt/pleroma`)
3. Run `sudo -Hu postgres pg_dump -d <pleroma_db> --format-custom -f </path/to/backup_location/pleroma.pgdump>`
4. Copy `pleroma.pgdump`, `config/prod.secret.exs`, and the `uploads` folder to your backup destination. If you have other modifications, copy those changes, too.
5. Restart the Pleroma service.

## Restore

1. Stop the Pleroma service.
2. Go to the working directory of Pleroma (default is `/opt/pleroma`)
3. Copy the above mentioned files back to their original position. 
4. Run `sudo -Hu postgres pg_restore -d <pleroma_db> -v -1 </path/to/backup_location/pleroma.pgdump>`
5. Restart the Pleroma service.

# Upgrading your instance

**Note:** Be sure to check for any additional requirements to satisfy
the upgrade: <https://pleroma.social/announcements/>

```bash
# stop pleroma
$ sudo systemctl stop pleroma
# cd to pleroma directory
$ cd /opt/pleroma
# pull changes
$ sudo -Hu pleroma git pull
# update deps
$ sudo -Hu MIX_ENV=prod mix deps.get
# run migrations (if any)
$ sudo -Hu MIX_ENV=prod mix ecto.migrate
# start pleroma
$ sudo systemctl start pleroma
```
