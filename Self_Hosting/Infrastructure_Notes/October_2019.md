---
title: October 2019
---

# 2019-10-01 - SSL Hardening

## aloy

| **Hosts** | Pleroma: https://splat.soy |

1. Scan with https://ssllabs.com/ssltest/
   1. Removed _TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_ cipher from _splat.soy.conf_
   2. Enabled TLSv1.3 in _splat.soy.conf_

**Note:** FastMail doesn't support DNS CAA records.

## chell

| **Hosts** | ZNC: https://znc.jrgnsn.net |

## jrgnsn-wp-01

|Hostname | Service |
| --- | --- |
| https://jrgnsn.net | Static blog |
| https://paste.jrgnsn.net | PrivateBin |
| https://playground.jrgnsn.net | Code Playground |
| https://rt.jrgnsn.net | Request Tracker |
| https://veganmsp.com | WordPress |
| https://wiki.jrgnsn.net | DokuWiki |

* jrgnsn.net
  * Removed protocols ''TLSv1'' and ''TLSv1.1'' from ''/etc/nginx/nginx.conf''
  * Added protocol ''TLSv1.3'' to ''/etc/nginx/nginx.conf''
  * Restarted nginx
  * Retested with SSLLabs
  * Modified ''/etc/letsencrypt/options-ssl-nginx.conf'' with better ciphers and protocols.
  * Restarted nginx
  * Retested with SSLLabs