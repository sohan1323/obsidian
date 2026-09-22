
---
Displays block-device attributes such as:

- UUID
- filesystem type
- filesystem label

### Syntax

```
blkid [OPTION] [DEVICE]
```

### Examples

```
sudo blkid
```

Example:

```
/dev/sda1: UUID="ABCD-1234" TYPE="vfat"
/dev/sda2: UUID="xxxx-xxxx" TYPE="ext4"
```

Specific device:

```
sudo blkid /dev/sda2
```

### Practical use

Find a partition's UUID:

```
sudo blkid /dev/sda2
```

UUIDs are commonly used in `/etc/fstab`.