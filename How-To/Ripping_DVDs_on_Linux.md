---
title: Ripping DVDs on Linux
---

# Install Required Packages

* libdvdcss
* libdvdcss2
* dvdread

```sh
sudo apt install libdvd-pkg
sudo dpkg-reconfigure libdvd-pkg
git clone https://github.com/xrgtn/dvdread.git /tmp/dvdread
cd /tmp/dvdread
make
sudo cp dvdread /usr/bin
```

# Create DVD ISO

```sh
dvdread /dev/cdrom >dvd.iso
```

# Mount ISO

```sh
sudo mkdir /media/iso
sudo mount dvd.iso /media/iso -o loop
```

# Processing Video Files

## With `ffmpeg`

```sh
cat /media/iso/VIDEO_TS/VTS_0*_*vob | ffmpeg -i - -vcodec h264 -acodec mp2 Movie.mp4
```

# See also
* [FFmpeg Tips & Tricks](/FFmpeg_Tips_&_Tricks)