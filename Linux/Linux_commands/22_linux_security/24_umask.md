
---
Controls default permission bits for newly created files/directories.

Check:

```
umask
```

Symbolic representation:

```
umask -S
```

Example:

```
u=rwx,g=rx,o=rx
```

A restrictive `umask` reduces default permissions.