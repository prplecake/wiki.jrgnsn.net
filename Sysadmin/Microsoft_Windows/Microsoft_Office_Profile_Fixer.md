---
title: Microsoft Office Profile Fixer
description: 
published: true
date: 2021-04-08T15:11:05.653Z
tags: microsoft, powershell, microsoft windows, microsoft office
editor: markdown
dateCreated: 2021-04-08T15:11:05.653Z
---

# Usage

1. Make sure all Microsoft Office applications are closed.
2. Run the script!

# Script

```powershell
$user = $env:username

$OfficePath = "C:\Users\$user\AppData\Local\Microsoft\Office"
if (Test-Path -Path $OfficePath) {
    Rename-Item $OfficePath "Office.old"
}
```

# Troubleshooting

## Rename-Item: Access to the path ...\Local\Microsoft\Office is denied.

There is still an open Office application somewhere or the script isn't being run with administrative rights.

1.  Close all Microsoft Office applications.
2.  Run the script as an administrator.

# TODO

* Add check to the script to warn if it detects there's open Office applications before trying to rename the folder.