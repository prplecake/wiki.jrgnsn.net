---
title: Asus RT-AX88U
---

# Excessive Requests to dns.msftncsi.com 

SSH or Telnet into the router and run the following commands:

```sh
$ nvram set dns_probe_content=0.0.0.0
$ nvram set dns_probe_host=""
$ nvram commit
$ reboot
```

# See also

* <https://discourse.pi-hole.net/t/excessive-requests-for-dns-msftncsi-com/556/6>
* <https://www.snbforums.com/threads/constant-unwanted-traffic-to-dns-msftncsi-com-from-rt-ac66u.35367/>
