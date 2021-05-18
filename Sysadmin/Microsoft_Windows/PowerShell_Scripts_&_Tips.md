---
title: PowerShell Script & Tips
description: 
published: true
date: 2021-04-08T14:58:10.460Z
tags: microsoft, windows, powershell, pwsh
editor: markdown
dateCreated: 2021-04-08T14:58:10.460Z
---

# Quickly Create Basic Authorization Header

```powershell
$Headers = @{ Authorization = "Basic {0}" -f [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("USERNAME:PASSWORD"))) }
```

You can use it like this:

```powershell
Invoke-WebRequest -Uri https://example.com -Headers $Headers -UseBasicParsing
```

# Filter and List Services

```powershell
Get-Service -Name SQL Anywhere | Select-Object -Property Name,Status,StartType | Where-Object {$_.StartType -eq "Automatic"} | Format -Table -auto
```

# Translating Usernames to/from SIDs

Source: https://www.morgantechspace.com/2015/09/convert-sid-to-username-using-powershell.html

## Convert Username to SID

The PowerShell below converts a username to a Security Identifier (SID). Replace the variable `$user` with your account to be translated.

```powershell
$user ='CONTOSO\jsmith'
$objUser = New-Object System.Security.Principal.NTAccount($user)
$objSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
Write-Host "Resolved user's sid: " $objSID.Value
```

## Convert SID to Username

The PowerShell below converts a Security Identifier (SID) to a user account. Replace the variable `$SID` with your own SID value to translate.

```powershell
$SID ='S-1-5-18'
$objSID = New-Object System.Security.Principal.SecurityIdentifier($SID)
$objUser = $objSID.Translate([System.Security.Principal.NTAccount])
Write-Host "Resolved user name: " $objUser.Value
```

This example should give a result of `NT AUTHORITY\SYSTEM`. 