
---
Attaches a filesystem to a directory called a **mount point**.

### Syntax

```
mount [OPTION] DEVICE MOUNT_POINT
```

### Examples

Show currently mounted filesystems:

```
mount
```

More readable:

```
mount | column -t
```

Mount a partition:

```
sudo mount /dev/sdb1 /mnt
```

Now:

```
cd /mnt
```

the contents of `/dev/sdb1` are accessible there.

Unmount:

```
sudo umount /mnt
```

### Important options

|Option|Purpose|
|---|---|
|`-t TYPE`|Specify filesystem type|
|`-o OPTIONS`|Specify mount options|
|`-a`|Mount filesystems from `/etc/fstab`|
|`-r`|Mount read-only|

Example:

```
sudo mount -o ro /dev/sdb1 /mnt
```

Mount read-only.

### Practical use

Forensic examination of a disk/partition can use read-only mounting:

```
sudo mount -o ro /dev/sdb1 /mnt
```