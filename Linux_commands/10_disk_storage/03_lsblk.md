
---
Already introduced in system information, but it is especially important for storage.

### Purpose

Lists block devices and their partition structure.

### Examples

```
lsblk
```

```
lsblk -f
```

```
lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINTS
```

Example:

```
NAME   SIZE FSTYPE TYPE MOUNTPOINTS
sda     80G        disk
├─sda1  512M vfat  part /boot/efi
└─sda2 79.5G ext4  part /
```