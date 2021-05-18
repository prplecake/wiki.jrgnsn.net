---
title: FFmpeg Tips & Tricks
---

# Split Video File

Sometimes I've found it necessary to spit video files, for example when one file contains multiple episodes.

```
ffmpeg -i input.mkv -vcodec copy -acodec copy -scodec copy -ss 00:00:00 -t 00:30:00 output1.mkv \
   -vcodec copy -acodec copy -scodec copy -ss 00:30:00 -t 00:30:00 output2.mkv
```

* `-i <filename>` - input filename
* `-vcodec copy` - copy video codec from source
* `-acodec copy` - copy audio codec from source
* `-scodec copy` - copy subtiles codec from source
* `-ss 00:00:00` - seek to given time position in seconds. "`hh:mm:ss[.xxx]`" syntax is also supported.
* `-t 00:30:00` - restrict the transcoded/captured video sequence to the duration specified in seconds. "`hh:mm:ss[.xxx]`" syntax is also supported.

# See also

* [FFmpeg Man Page](https://linux.die.net/man/1/ffmpeg)