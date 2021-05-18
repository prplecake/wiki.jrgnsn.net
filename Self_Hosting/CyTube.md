---
title: CyTube
---

> Node.JS Server and JavaScript/HTML Client for synchronizing online media
>     - [CyTube repo](https://github.com/calzoneman/sync)

The project documentation is lacking and includes a warning saying so. If you happen across my documentation here, I hope it can be of use to you.

To get TLS working I linked the certificate and public keys from Let's Encrypt's directories.

```
sudo ln -s /etc/letsencrypt/live/cytube.splat.soy/privkey.pem /opt/cytube/privkey.pem
sudo ln -s /etc/letsencrypt/live/cytube.splat.soy/fullchain.pem /opt/cytube/fullchain.pem
```

See: [Allow Non-Root Access to Let's Encrypt Certificates](/Sysadmin/KB/Allow_Non-Root_Access_to_Let's_Encrypt_Certificates)

## See also

* [/Config files](/Self_Hosting/CyTube/Config_files)