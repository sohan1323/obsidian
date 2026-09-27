
---
Identifies processes using filesystems/files.

```
fuser /mnt
```

Verbose:

```
fuser -v /mnt
```

Filesystem:

```
sudo fuser -vm /mnt
```

TCP port:

```
sudo fuser -n tcp 22
```
