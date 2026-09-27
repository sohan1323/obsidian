
---
A mounted filesystem can sometimes be remounted read-only:

```
sudo mount -o remount,ro /mountpoint
```

Return to read-write:

```
sudo mount -o remount,rw /mountpoint
```

Whether this is safe depends on the filesystem and what processes are using it.