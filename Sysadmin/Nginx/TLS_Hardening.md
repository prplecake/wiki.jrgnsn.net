---
title: Nginx - TLS Hardening
---

# Configure HSTS on Nginx

Add the following to the server block of your HTTPS configuration:

```nginx
add_header Strict-Transport-Security max-age=31536000;
```

**Caution!** This will cause the browser to cache the header for about one year. Use a shorter `max-age` for testing.

# Other Useful HTTP Headers

```nginx
ssl_prefer_server_ciphers On;
ssl_protocols TLSv1.1 TLSv1.2;
ssl_ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:!RSA+AES:!aNULL:!MD5:!DSS;
```

# Additional Resources
* [Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)
* [How to configure HTTP Strict Transport Security (HSTS) on Apache & NGINX](https://itigloo.com/security/how-to-configure-http-strict-transport-security-hsts-on-apache-nginx/)
