---
title: Matrix Server
---

I'm running [matrix-synapse](https://matrix.org/docs/projects/server/synapse/) on my homeserver.

# Nginx config

```nginx
server {
    listen 80;
    server_name matrix.domain.tld;
    location / {
        proxy_pass http://localhost:8008;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```