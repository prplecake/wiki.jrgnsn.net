---
title: Pi-hole Incident: March 2020
---

I set up a Pi-hole on a much better server than my [Raspberry Pi](/Sysadmin/Raspberry_Pi)s have ever made.

The server is a Dell OptiPlex 745.

|---|---|
|**OS** | Debian 10 (buster) x64|
|**Kernel** | 4.19.0-8-amd64|
|**CPU** | Intel Pentium D 2 @ 3.40GHz|
|**RAM** | 4 GB|
|**/dev/sda** | 80 GB|

# 03-07 Incident

The server suffered several hard restarts while my brother was working on lighting in the basement. The server needs a new mainboard battery, and thus did not come back up until manual intervention[^1].

However, when the server did finally boot back into Debian, DNS did not work.

That said, looking at the server on 2020-03-14, the server is nominal.

[^1]:I had to strike <kbd>F1</kbd>. 