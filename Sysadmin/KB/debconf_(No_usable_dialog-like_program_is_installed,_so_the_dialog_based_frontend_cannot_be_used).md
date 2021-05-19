---
title: "debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used."
---

# Error

> debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)

# Resolution

Install dialog:
```sh
$ sudo apt install dialog
```
