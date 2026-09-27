
---
Checks whether a directory is a mount point.

```
mountpoint /mnt
```

Quiet test:

```
mountpoint -q /mnt
```

Then:

```
echo $?
```

`0` means it is a mount point.