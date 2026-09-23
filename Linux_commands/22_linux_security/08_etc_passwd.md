
---
Contains account information.

```
cat /etc/passwd
```

Typical format:

```
username:x:UID:GID:comment:home:shell
```

Example:

```
alice:x:1000:1000:Alice:/home/alice:/bin/bash
```

Fields:

```
1 username
2 password placeholder
3 UID
4 GID
5 comment/GECOS
6 home directory
7 login shell
```

Passwords are normally not stored directly here.