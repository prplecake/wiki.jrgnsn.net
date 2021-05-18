---
title: WeeChat Tips
---

# How to use command line/input bar with more than one line?

The option `size` in input bar can be set to a value higher than 1 (for fixed size, default size is 1) or 0 for dynamic size, and then option `size_max` will set the max size (0 = no limit).

Example with dynamic size:

```
/set weechat.bar.input.size 0
```

Max size of two:

```
/set weechat.bar.input.size_max 2
```

# Aliases

ZNC detach and buffer close:

```
/alias add /dc /znc detach $channel; /close
```

> Note: this will only work once you enable send_unknown_commands:
{.is-info}


```
/set irc.network.send_unknown_commands on
```

* Ref: https://wiki.znc.in/Weechat#Enabling_.2FZNC_and_other_raw_commands