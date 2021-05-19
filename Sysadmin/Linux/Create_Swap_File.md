---
title: Linux - Create Swap File
---

1. Create a file that will be used for swap:
```
$ sudo fallocate -l 1G /swapfile
```
2. Set permissions, only the root user should be able to access this file:
```
$ sudo chmod 600 /swapfile
```
3. Use `mkswap` to make the file swap space:
```
$ sudo mkswap /swapfile
```
4. Turn on swapping:
```
$ sudo swapon /swapfile
```

# See also
* [[Recommended System Swap Space|/Sysadmin/Linux/Recommended_System_Swap_Space]]
