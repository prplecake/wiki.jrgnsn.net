---
title: Common Commands
---

# apt

## Install Debian Package via CLI

To install a `.deb`: `sudo dpkg -i $DEB_PACKAGE`

Install package dependencies: `sudo apt --fix-broken install`

## List Installed Packages by Size 

```sh
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n
```

Unfortunately, on some systems, this list includes packages that have been removed but not purged. All such packages can be purged with:

```sh
dpkg --list |grep "^rc" | cut -d " " -f 3 | xargs sudo dpkg --purge
```

Or, if you don't want to purge uninstalled packages, you can use this variant to filter out the packages which aren't in the 'installed' state:

```sh
dpkg-query -Wf '${db:Status-Status} ${Installed-Size}\t${Package}\n' | sed -ne 's/^installed //p'|sort -n
```

More information: <https://unix.stackexchange.com/a/107039/134902>

# User Creation/Deletion

Create new user from the root shell: `useradd -m <username>``

Options:
* `-m` - creates the home directory for the user
* `-G` - _appends_ groups to the user

Delete a user from the root shell: <code>userdel <username></code>

# Get System Info

`uname` - prints system information
* `uname -a` - print all information
* `uname -s` - print the kernel name
* `uname -r` - print the kernel release
* `uname -v` - print the kernel version
* `uname -m` - print the machine hardware name
* `uname -p` - print the processor type
* `uname -i` - print the hardware platform
* `uname -o` - print the operating system

## OS Specific Versions

* **CentOS:** `cat /etc/centos-release`
* **Debian:** `cat /etc/debian_version`
* **Generic:** `cat /etc/issue`

# grep

```sh
grep -rnw 'PATH/TO/SEARCH' -e 'PATTERN'
```