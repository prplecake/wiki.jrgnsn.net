---
title: Raspberry Pi
---

# Headless Setup

Setting up a Raspberry Pi without a keyboard, mouse, or display is easy!

SSH is disabled by default in Raspbian. To enable SSH, simply place a file called `ssh` in the root of the boot folder on your Raspbian SD card.

## Wireless Configuration

Place the following in a file called `wpa_supplicant.conf` in the boot folder.

```
country=<insert country code here>
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="<Name of your WiFi network>"
    psk="<Password for your network>"
}
```

# Additional Information

* <https://www.raspberrypi.org/documentation/configuration/wireless/headless.md>

# See also

* [Self hosting Pi-hole](/Self_Hosting/Pi-hole)