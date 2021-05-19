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

# Unbound configuration

Based on https://docs.pi-hole.net/guides/unbound/#configure-unbound
```config
server:
    # If no logfile is specified, syslog is used
    # logfile: "/var/log/unbound/unbound.log"
    verbosity: 0

    port: 5353
    do-ip4: yes
    do-udp: yes
    do-tcp: yes

    # May be set to yes is you have IPv6 connectivity
    do-ip6: no

    # Use this only when you downloaded the list of primary root
    # servers!
    root-hints: "/var/lib/unbound/root.hints"

    ## Trust glue only if it is within the server's authority
    harden-glue: yes

    # Require DNSSEC data for trust-anchored zones, if such data
        # is absent, the zone becomes BOGUS
    harden-dnssec-stripped: yes

    # Don't use Capitalization randomization as it known to cause
        # DNSSEC issues sometimes
    # see https://discourse.pi-hole.net/t/unbound-stubby-or-dnscrypt-proxy/9378
        # for further details
    use-caps-for-id: no

    # Reduce EDNS reassembly buffer size.
    # Suggested by the unbound man page to reduce fragmentation reassembly problems
    edns-buffer-size: 1472

    # Perform prefetching of close to expired message cache entries
    # This only applies to domains that have been frequently queried
    prefetch: yes

    # One thread should be sufficient, can be increased on beefy machines. In reality for most users running on small networks or on a single machine, it should be unnecessary to seek performance enhancement by increasing num-threads above 1.
    num-threads: 1

    # Ensure kernel buffer is large enough to not lose messages in traffic spikes
    so-rcvbuf: 1m

    # Ensure privacy of local IP ranges
    private-address: 192.168.0.0/16
    private-address: 169.254.0.0/16
    private-address: 172.16.0.0/12
    private-address: 10.0.0.0/8
    private-address: fd00::/8
    private-address: fe80::/10
```

# See also

* [[pi-hole.conf|/Self_Hosting/Pi-hole/pi-hole.conf]]