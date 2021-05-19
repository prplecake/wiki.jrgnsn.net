---
title: Backup and Restore NTFS Disk
---

NTFS is the most common file system for Windows devices.

# Listing Drives/Volumes

The first step is to detect the partition your data are located on. To detect disks and partitions, run the following command: `fsarchiver probe simple`.

You can also list partitions with `cat /proc/partitions`, or use [GParted](https://gparted.org/).

# Mounting the Partition

## Read-only Support

Now, let's make this data accessible to the system. If you're simply taking a backup, RO access is all you need, and that can be achieved with either of the following commands:

```sh
ntfs-3g -o ro /dev/sda1 /mnt/windows
```

```sh
mount -t ntfs /dev/sda1 /mnt/windows -o ro
```

Where `/dev/sda1` is the name of the disk discovered with `fsarchiver`.

## Read-Write Support

If you need full Read-Write support, you'll have to use a userspace program, [ntfs-3g](https://www.tuxera.com/community/open-source-ntfs-3g/)[^1]

[^1]:ntfs third generation driver

Simply:

```sh
ntfs-3g /dev/sda1 /mnt/windows
```

# Creating a Backup

Once you know what drive you're backing up, and where you're backing it up to:

```sh
ntfsclone --save-image --output backup.img /dev/sda1
```

Where `backup.img` is the name of the file to write the data to, and `/dev/sda1` is the partition to copy.

* [ntfsclone man pages](https://linux.die.net/man/8/ntfsclone)

# Restoring a Backup

```sh
ntfsclone --restore-image --overwrite /dev/sda1 backup.img
```
