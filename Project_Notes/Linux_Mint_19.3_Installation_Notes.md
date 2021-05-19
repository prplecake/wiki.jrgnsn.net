---
title: Linux Mint 19.3 Installation Notes
---

Linux Mint - <https://linuxmint.com/>

* Installing Linux Mint Cinnamon Edition
* Linux Kernel 5.0[^1]

[^1]:<https://www.linuxmint.com/rel_tricia_cinnamon_whatsnew.php#system>

# Immediate Gotchas
* Linux Mint requires at least 10G of disk space.

# Installation Notes
* Opted to not "Install third-party software for graphics, Wi-Fi hardware, Flash, MP#, and other media"
* Letting the installer "Erase disk and install Linux Mint"

## VMware Tools

VMware tools never seems to be able to install itself right with the scripts provided. Here's what I did:

1. In VMware Workstation, navigate to **VM** -> **Install VMware Tools...** to mount the CD in the guest.
2. Copy the `.tar.gz` file to my desktop.
3. Extract with `tar xzvf VMwareTools-10.3.10-13959562.tar.gz`
4. Hop into the new directory: `cd vmware-tools-distrib`
5. Run the install script: `sudo ./vmware-install.pl`
6. Accept defaults.
7. Clean up. `cd ..;rm VMwareTools-10.3.10-13959562.tar.gz;rm -rf vmware-tools-distrib`

## VMware Tools Gotchas

### vmxnet driver
```
The vmxnet driver is no longer supported on kernels 3.3 and greater. Please upgrade to a newer virtual NIC. (e.g., vmxnet3 or e1000e)
```

# Configuring System

## Video Issues

Immediately I'm noticing cinnamon uses _a lot_ of CPU. I'm missing some graphics drivers.

I simply had to check the **Accelerate 3D graphics** in the VM Settings.

![Linux mint vmware accelerate 3d graphics](/Project_Notes/Linux_Mint_19.3_Installation_Notes/Linux_mint_vmware_accelerate_3d_graphics.png)

I also increased the amount of Graphics memory from 128 MB to 768 MB.

## Changing apt sources

Linux Mint 19.3 comes with `bionic` sources by default. I'm attempting to upgrade them to `eoan`.

I changed my `/etc/apt/sources.list.d/official-package-repositories.list` from:
```
deb http://packages.linuxmint.com tricia main upstream import backport 

deb http://archive.ubuntu.com/ubuntu bionic main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu bionic-updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu bionic-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://archive.canonical.com/ubuntu/ bionic partner
```

to:

```
deb http://packages.linuxmint.com tricia main upstream import backport 

deb http://archive.ubuntu.com/ubuntu eoan main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu eoan-updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu eoan-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ eoan-security main restricted universe multiverse
deb http://archive.canonical.com/ubuntu/ eoan partner
```

Then ran: `sudo apt update;sudo apt upgrade`