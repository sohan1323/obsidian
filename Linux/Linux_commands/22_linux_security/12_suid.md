
---
SUID causes an executable to run with the file owner's effective UID.

Find SUID files:

```
find / -type f -perm -4000 2>/dev/null
```

Check one:

```
ls -l /path/to/file
```

Example:

```
-rwsr-xr-x
```

The `s` in the owner execute position indicates SUID.