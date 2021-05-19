---
title: Pleroma
---

| **Software** | Pleroma |
| **Branch** | Develop |
| **Current URL** | <https://jrgnsn.social> |


I've decided to start using [Pleroma](https://pleroma.social/) instead of [Mastodon](https://joinmastodon.org/), specifically for the lighter footprint. It was after reading [this article](https://blog.soykaf.com/post/what-is-pleroma/) that I made my decision. 

<del>The new instance of Pleroma will live at https://splat.soy.</del>

Pleroma's documentation isn't the greatest, and I've learned a lot since I've started using Pleroma that's not documented anywhere else[^1].

[^1]:besides various posts on the fediverse

# Notes

I used Pleroma's [Installing on Linux using OTP releases](https://docs-develop.pleroma.social/backend/installation/otp_en/) guide.

Setup was pretty straightforward. Once Pleroma was up and running, I made sure to disable registrations and enable invitations. Since I'm not following the develop branch on Pleroma, I'm not sure the invite API is implemented yet, but I can generate invite links on the command-line. 

OTP releases keep their configuration at `/etc/pleroma/config.exs`

```elixir
config :pleroma, :instance,
    ...
    registrations_open: false,
    invites_enabled: true,
    ...
```

I then went through Pleroma's own security hardening guide: <https://docs-develop.pleroma.social/backend/configuration/hardening/>

# Configuration

## Disabling Chat

To disable chat, add the following to your configuration file[^2]:

[^2]:`/etc/pleroma/config.exs` or `/opt/pleroma/config/prod.secret.exs`

```elixir
config :pleroma, :chat,
  enabled: false
```

## Custom Emoji

For the most part, Pleroma's own docs are a good start: <https://docs-develop.pleroma.social/backend/configuration/custom_emoji/>

When I was done with Pleroma's docs, all I had was a bunch of emojis on my filesystem. The docs failed to mention that configuration is still required. So in your configuration file[^2]:

```elixir
config :pleroma, :emoji,
  groups: [
    Blobs: "/blogs.gg/*.png",
  ]
```

### Larger Emoji

**Note:** As of at least Pleroma 2.0.7, larger emojis are shown on pleroma-fe.

For masto-fe, add the following CSS to `common.css`:

```css
.reply-indicator__content .emojione,
.status__content .emojione {
    width: 30px !important;
    height: 30px !important;
    margin: 0 !important;
}
```

`common.css` might be found somewhere like `/opt/pleroma/lib/$PLEROMA_VERSION/priv/static/core/common.css`


## [[Setting up Object Storage|/Self_Hosted/Pleroma/Setting_up_Object_Storage]] 

# Customization

## Changing Default Theme

I had a bit of trouble figuring out how to change the default theme of my instance. Fortunately, there's some awfully helpful people on the fediverse to fill in the holes the documentation has.

The first thing I did was create a theme I like. I did this using Pleroma's theme web interface. Then I downloaded the JSON file and threw it on my server. The JSON file should end up in the `static/themes` directory. On my OTP installation, that was `/var/lib/pleroma/static/static/themes/`. **Note:** you may need to create that directory.

Now that I had my theme on the server, I needed to tell Pleroma to use it. You customize Pleroma-FE with Pleroma's BE configuration. My configuration looks somethining like this:

```elixir
config :pleroma, :frontend_configurations,
  pleroma_fe: %{
    theme: "pleroma-purple"
  }
```

I also had to create `/var/lib/pleroma/static/static/styles.json`: (I used Pleroma's default and just added my theme to it.)

You can find pleroma's default here: <https://git.pleroma.social/pleroma/pleroma/blob/stable/priv/static/static/styles.json>

Once you add your theme to `styles.json`, you should see it appear in the themes dropdown in your instance's settings web interface.

## Default Post Content Type
* <https://docs.pleroma.social/frontend/CONFIGURATION/#postcontenttype>

```elixir
config :pleroma, :frontend_configurations,
  pleroma_fe: %{
    ...
    postContentType: "text/markdown"
  }
```

Where `postContentType` is one of:
* `text/plain` - _default_
* `text/html`
* `text/markdown`
* `text/bbcode`

**Note:** If you have `config :pleroma, :configurable_from_database, true`, you'll have to make this change in `/etc/pleroma/config.exs`, migrate it to your database, then restart your Pleroma instance. There currently isn't a field on the Settings page in admin-fe to modify this setting.

### Notes
* I haven't found a way to default the post type for masto-fe that comes bundled with Pleroma OTP.

## Instance Panel

Location for OTP installations:
* `/var/lib/pleroma/static/instance/panel.html`

The default panel includes some HTML which is below so you can mimic the look:

```html
<div style="margin-left:12px; margin-right:12px;">
    <!-- your code here -->
</div>
```

This is the instance panel on splat.soy:

```html
<div style="margin-left:12px; margin-right:12px;">
    <p><strong>Welcome to Pleroma/splat.soy!</strong></p>
    <p>This is a private instance. If you know me personally, feel free to
    contact me for an invitation.</p>
    <p><a href="/announcements">Server Announcements</a><br />
    Server Admin: <a href="/AstroBadger">@AstroBadger</a></p>
    <p><a href="/main/all">Pleroma FE</a> | <a href="/web">Mastodon FE</a> | <a href="/about">About</a></p>
</div>
```

## MastoFE Mascot

Add something like the following to your `/etc/pleroma/config.exs`:

```elixir
config :pleroma, :assets,
  mascots: [
    turtle: %{
      mime_type: "image/png",
      url: "/images/turtle.png"
    }
  ],
  default_mascot: :turtle
```

Then be sure to place `turtle.png` under `/var/lib/pleroma/static/images/`.

## Terms of Service

Most instances I've seen use the Terms of Service page as an extended instance panel.

Location for OTP installations:
* `/var/lib/pleroma/static/static/terms-of-service.html`

# Backup/Restore your instance

## Backup

  

1. Stop the Pleroma service.
2. Go to the working directory of Pleroma (default is `/opt/pleroma`)
3. Run `sudo -Hu postgres pg_dump -d <pleroma_db> --format=custom -f </path/to/backup_location/pleroma.pgdump>`
4. Copy `pleroma.pgdump`, `/etc/pleroma/config.exs`, and the `uploads` folder to your backup destination. If you have other modifications or customization, copy those changes, too.
5. Restart the Pleroma service.

## Restore 

1. Stop the Pleroma service.
2. Go to the working directory of Pleroma (default is `/opt/pleroma`)
3. Copy the adove mentioned files back to their original position. 
4. Run `sudo -Hu postgres pg_restore -d <pleroma_db> -v -1 </path/to/backup_location/pleroma.pgdump>`
5. Restart the Pleroma service.

**Note:** I've had issues restoring with the `pg_restore` command, so instead I've used the following command to restore Pleroma's database:

```
$ sudo -Hu postgres psql -d pleroma < pleroma.pgdump
```

**Note:** I've noticed it can take a _very long_ time for postgres to recreate indexes. It might be helpful to tune postgres to your server before restoring the database:[^3] <https://pgtune.leopard.in.ua/>

[^3]:I didn't do this, and it took about an hour and a half to restore a 4G database on a fairly beefy server: 4@2.2GHz, 16G RAM, though it was painfully clear postgres wasn't using nearly as many resources as it could have.

#### Hosting Multiple Instances on a Single Host

**To do:** Write this section.
