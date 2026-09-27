
---
Informs the kernel about changes to a disk's partition table.

### Syntax

```
sudo partprobe [DEVICE]
```

### Example

```
sudo partprobe /dev/sdb
```

### Practical use

After changing a partition table, you may need:

```
sudo partprobe /dev/sdb
```

so the kernel rereads the partition table.