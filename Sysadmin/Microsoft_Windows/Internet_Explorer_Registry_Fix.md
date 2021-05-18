---
title: Internet Explorer Registry Fix
---

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\MAIN\FeatureControl\FEATURE_ENABLE_PRINT_INFO_DISCLOSURE_FIX]
"iexplore.exe"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Internet Explorer\MAIN\FeatureControl\FEATURE_ENABLE_PRINT_INFO_DISCLOSURE_FIX]
"iexplore.exe"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\MAIN\FeatureControl\FEATURE_ALLOW_USER32_EXCEPTION_HANDLER_HARDENING]
"iexplore.exe"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Internet Explorer\MAIN\FeatureControl\FEATURE_ALLOW_USER32_EXCEPTION_HANDLER_HARDENING]
"iexplore.exe"=dword:00000001
```