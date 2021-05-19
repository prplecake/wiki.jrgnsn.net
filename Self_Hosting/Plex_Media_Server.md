---
title: Plex Media Server
---

I run the [Plex media server](https://www.plex.tv/) on one of my machines. With [FileBot](https://www.filebot.net/) to manage renaming and organizing media for me, this is a really simple solution.

# Automated Media Center with FileBot

* [Automated Media Center (FileBot forums)](https://www.filebot.net/forums/viewtopic.php?t=215)

I saved the script [located here](https://github.com/filebot/plugins/blob/master/bash/amc.sh) to `~/amc.sh`, made it executable, then set up cron like so:

```
*/15 * * * * find /path/to/media/to/process -type f -not -iname '*.part' -exec ~/amc.sh {} +
```

As stated on the forum post:

* Movies will be sorted into `{output}/Movies/Name (Year)/Name (Year) [CD123].ext`
* TV Shows will be sorted into `{output}/TV Shows/Name/Season N/Name - S00E00 - Title.ext`
* Music will be sorted into `{output}/Music/Artist/Album/Artist - Title.ext`

**Note:** The above directions are now obsolete on my media server. I've switched to a slightly different script to "sync" torrents from my seedbox.

# Automation

I've got scripts set up with cron to automate pulling stuff down from my seedbox. You can find `amc.sh` and `lftp_sync` [at the repository](https://github.com/prplecake/media-server-scripts).

You can also find some [rtorrent customizations](https://github.com/prplecake/media-server-scripts/blob/master/seedbox/rtorrent.rc.custom) in that repo. These customizations create a hardlink to completed torrents. This allows me to continue to seed torrents while maintaining the ability to keep track of what's been downloaded from the seedbox.

## `amc.sh``

I keep mine at `~/amc.sh`

```shell
#!/bin/sh -xu
filebot -script fn:amc --output "/mnt/Media" --action copy --conflict skip \
    -non-strict --log-file amc.log --def excludeList=".excludes" unsorted=y music=y artwork=y "$@"
```

### Additional Options 

The following are useful for small episodes.
* `--def minFileSize=0` - Only process video files larger than the given number (in bytes). Defaults to 50 MB.
* `--def minLengthMS=0` - Only process videos longer than the given number (in milliseconds). Defaults to 10 minutes.

### See also 
* [FileBot CLI usage manual](https://www.filebot.net/cli.html)
* [FileBot - [Docs] Use --mapper expressions for AniDB / TheTVDB cross-entity matching](https://www.filebot.net/forums/viewtopic.php?t=10996)
* [FileBot - Automated Media Center](https://www.filebot.net/forums/viewtopic.php?t=215)

## `lftp_sync`

`lftp_sync` is a script to automate downloading completed torrents from my seedbox. It uses `lftp`, which is widely available on Linux distros, to download over the SSH protocol. In the script you'll notice there's variables for a username and password, but I instead have the seedbox SSH details configured in `~/.ssh/config`.

I feel this is secure enough, since my ISP would only ever see SSH traffic, which is encrypted.

# See also

* [media-server-scripts](https://github.com/prplecake/media-server-scripts)
* [FFmpeg Tips & Tricks](/FFmpeg_Tips_&_Tricks)