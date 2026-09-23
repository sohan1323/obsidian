
---
Find SGID files:

```
find / -type f -perm -2000 2>/dev/null
```

Directory SGID is also important.

```
ls -ld directory
```

Example:

```
drwxrwsr-x
```

For a directory, SGID causes newly created files to inherit the directory's group in normal configurations.