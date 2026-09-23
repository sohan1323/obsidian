
---
Unmount a filesystem:

```
sudo umount /mnt
```

Or:

```
sudo umount /dev/sdb1
```

If a filesystem is busy:

```
sudo fuser -vm /mnt
```

Find processes using it before attempting to unmount.