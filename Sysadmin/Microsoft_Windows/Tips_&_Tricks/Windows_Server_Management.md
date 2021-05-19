---
title: Windows Server Management
---

# Add Computer to Domain via PowerShell

```powershell
Add-Computer -Domain DOMAIN_NAME -Credential DOMAIN_ADMIN
```

Where:
* `DOMAIN_NAME` is the name of the domain to join; and,
* `DOMAIN_ADMIN` is a domain administrator user account

# Rename Computer via PowerShell

```powershell
Rename-Computer -NewName NEW_HOSTNAME
```

Where:
* `NEW_HOSTNAME` is the new desired computer name

Optional:
* Provide the `-Credential` flag to pass admin privileges if not admin.
