
---
Unmounts a mounted filesystem.

### Syntax

```
umount [OPTION] MOUNT_POINT
```

### Examples

```
sudo umount /mnt
```

Or:

```
sudo umount /dev/sdb1
```

Force/lazy behavior:

```
sudo umount -l /mnt
```

### Important option

|Option|Purpose|
|---|---|
|`-l`|Lazy unmount|
|`-R`|Recursively unmount|

If you get:

```
target is busy
```

check which process is using it:

```
sudo lsof /mnt
```

or:

```
sudo fuser -vm /mnt
```