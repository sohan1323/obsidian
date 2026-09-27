
---
Creates, deletes, resizes, and examines partitions.

It supports modern **GPT** partition tables.

### Syntax

```
sudo parted [OPTION] [DEVICE]
```

### Examples

Show all disks:

```
sudo parted -l
```

Open a disk:

```
sudo parted /dev/sdb
```

Inside:

```
print
```

shows the partition table.

Create GPT partition table:

```
mklabel gpt
```

Create partition:

```
mkpart
```

### Practical use

Partition inspection:

```
sudo parted -l
```