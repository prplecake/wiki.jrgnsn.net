---
title: Import/Export PGP key pair
---

# Export

```sh
$ gpg --list-keys
/home/user/.gnupg/pubring.gpg
--------------------------------
pub 1024D/ABCDFE01 2008-04-13
uid firstname lastname (description) <email@example.com>
sub 2048g/DEFABC01 2008-04-13
```

Export key `ABCDFE01`:
```sh
$ gpg --output gpgkey_pub.gpg --armor --export ABCDFE01
$ gpg --output gpgkey_sec.gpg --armor --export-secret-key ABCDFE01
```

Optionally, use `scp` to copy those files to a remote host:
```sh
$ scp gpgkey_pub.gpg gpgkey_sec.gpg user@remotehost:~/
```

# Import

On the _"import host"_:
```sh
$ gpg --import ~/gpgkey_pub.gpg
$ gpg --import ~/gpgkey_sec.gpg
```

**Note:** Don't forget to remove the exposed keys: `$ rm ~/gpgkey_*`