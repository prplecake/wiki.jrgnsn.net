---
title: Create A Bootable Debian USB Install Disk on macOS
---

# Convert the Debian ISO to an IMG File

```sh
$ hdiutil convert -format UDRW -o /path/to/output-file.img /path/to/input.iso
```

The resulting file might have `.dmg` appended to it, this is fine.

Run `diskutil list` to figure out which disk is your USB drive. Typically in later versions of macOS it can be `/dev/disk2`.

Whichever disk it is, unmount it:

```sh
$ diskutil unmountDisk /dev/disk2
```

# Write the Operating System to the USB Drive

```sh
$ sudo dd if=/path/to/inputfile.img of=/dev/rdisk2 bs=1m
```

This can take awhile, I like using `progress` to monitor `dd`.

Once this is complete, you can use this USB drive to boot into Debian.

On your Mac, you may get an alert that "the disk you inserted was not readable by this computer." This is fine.

# See also

* [How to Create a Bootable Debian USB Drive on MacOS](https://zerotoroot.me/create-bootable-debian-usb-drive-macos/)
