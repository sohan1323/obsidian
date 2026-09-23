
---
Displays block-device attributes.

```
sudo blkid
```

Example information:

```
/dev/sda1: UUID="..." TYPE="ext4"
/dev/sda2: UUID="..." TYPE="swap"
```

Specific device:

```
sudo blkid /dev/sda1
```