---
title: Arch Linux Installation Notes
---

About two years ago I took my first crack at installing [Arch Linux](https://www.archlinux.org/) on a spare computer. These notes are by no means complete, and I wish I would've taken better, more complete notes.

# Notes

Machine I Used: Dell Latitude E6520

## Network Configuration

no dhcp on boot, wired connection, no internet access

Ethernet controller
Kernel driver in use: e1000e

Device names:
* `eno1` - ethernet
* `wlp250` - wireless

Ran `systemctl start dhcpd.service`

`ping google.com`... success!

## Update System Clock

```sh
$ timedatectl set-ntp true
$ timedatectl status
```

## Partition the Disks

```
Disk        Size    Purpose
/dev/sda1   5G      swap
/dev/sda2   460.8G  /
```
