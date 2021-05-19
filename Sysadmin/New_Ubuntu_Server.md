---
title: New Ubuntu Server
---

Initializing Ubuntu Server...

Version...Ubuntu 18.04 Minimal

**Note:** This article assumes you already have SSH and root access on your new Ubuntu box.

Install favorite packages:
```sh
apt install git tmux zsh thefuck vim
```

Add my user and set up default shell, add to `sudo` group, then switch to it. As root:
```sh
adduser mjorgensen
chsh -s /bin/zsh mjorgensen
usermod -G sudo mjorgensen
su mjorgensen
```

Then I clone my dotfiles and use them:
```sh
$ git clone https://github.com/prplecake/dotfiles ~/.dotfiles
$ ~/.dotfiles/scripts/bootstrap
```

# Minimal Installation Gotchas

Ubuntu 18.04 Minimal doesn't seem to have the right tools to set locale correctly. As root:
```sh
apt install locales tzdata
dpkg-reconfigure locales
```
