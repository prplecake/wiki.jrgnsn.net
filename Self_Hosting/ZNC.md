This page has information regarded to installing and running ZNC itself.

# Auto-Deploy Let's Encrypt Certificates to ZNC

Add something like this to `cron`:

```
0 0 1 */1 * certbot renew --deploy-hook /home/<USERNAME>/.znc/scripts/deploy-certbot-post
```

**deploy-certbot-post**:
```bash
#!/bin/bash
cat /etc/letsencrypt/live/<DOMAIN_NAME>/{privkey,fullchain}.pem > /home/<USERNAME>/.znc/znc.pem
```
