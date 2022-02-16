[[_TOC_]]

# Install realmd

```
sudo apt install realmd
```

## Join a Domain

```
sudo realm join fortressmedical.com --user <AdminUser>
```

# Installing Kerberos Utilities

This was necessary on MLJ's Linux Mint machine to be able to mount SMB shares.

```
sudo apt install krb5-user krb5-config cifs-utils keyutils
```

```
 ┌──────────────────┤ Configuring Kerberos Authentication ├──────────────────┐
 │ When users attempt to use Kerberos and specify a principal or user name   │ 
 │ without specifying what administrative Kerberos realm that principal      │ 
 │ belongs to, the system appends the default realm.  The default realm may  │ 
 │ also be used as the realm of a Kerberos service running on the local      │ 
 │ machine.  Often, the default realm is the uppercase version of the local  │ 
 │ DNS domain.                                                               │ 
 │                                                                           │ 
 │ Default Kerberos version 5 realm:                                         │ 
 │                                                                           │ 
 │ CONTOSO.COM______________________________________________________________ │ 
 │                                                                           │ 
 │                                  <Ok>                                     │ 
 │                                                                           │ 
 └───────────────────────────────────────────────────────────────────────────┘ 
```

If you're presented with the following option regarding DNS servers, choose **No**.

```
 ┌──────────────────┤ Configuring Kerberos Authentication ├──────────────────┐
 │                                                                           │
 │ Typically, clients find Kerberos servers for their default realm in the   │
 │ domain-name system. Servers for your realm were found in DNS. For most    │
 │ configurations it is best to use DNS to find these servers so that if     │
 │ the set of servers for your realm changes, you need not reconfigure each  │
 │ machine in the realm. However, in special situations, you can locally     │
 │ configure the set of servers for your Kerberos realm.                     │
 │                                                                           │
 │ Add locations of default Kerberos servers to /etc/krb5.conf?              │
 │                                                                           │
 │                    <Yes>                       <No>                       │
 │                                                                           │
 └───────────────────────────────────────────────────────────────────────────┘
```

# See also

* [Linux: Mount a Windows share with kerberos authentication](https://michlstechblog.info/blog/linux-mount-a-windows-share-with-kerberos-authentication/)