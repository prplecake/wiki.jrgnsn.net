---
title: Unbound
---

# Pi-hole as All-Around DNS Solution

<https://docs.pi-hole.net/guides/unbound/>

# ASUS Router (router.asus.com)

ASUS publishes a DNS A record for router.asus.com with the data `192.168.0.1`.

I added this to my Unbound config, update to match your network's subnet:
```
local-data: "router.asus.com A 192.168.241.1"
local-data-ptr: "192.168.241.1 router.asus.com"
```

# Plex DNS Record Fix

Pi-hole + Unbound can break Plex's Direct Connect, or the ability to discover players advertising in the network. This is something to do with DNS Rebinding.[^1]

[^1]:<https://support.plex.tv/articles/206225077-how-to-use-secure-server-connections/#dnsrebinding>

Add a line like this to your Unbound config[^2]:
```
private-domain: plex.direct
```

[^2]:<https://www.reddit.com/r/PleX/comments/8oadfw/pihole_and_direct_connect/e02e595/>

# See also

* [[pi-hole.conf|/Self_Hosting/Pi-hole/pi-hole.conf]]