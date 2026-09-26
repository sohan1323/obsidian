
---
`diskpart` is Windows' command-line disk and partition management utility.

### Start DiskPart

```
diskpart
```

You will enter:

```
DISKPART>
```

Commands below are entered inside DiskPart.



# `diskpart list`

Displays available storage objects.

### List disks

```
list disk
```

Example:

```
Disk ###  Status         Size
--------  -------------  -------
Disk 0    Online          476 GB
Disk 1    Online           80 GB
```

### List volumes

```
list volume
```

Shows:

- Volume number
- Drive letter
- Label
- Filesystem
- Size
- Status

### List partitions

```
list partition
```

Usually used after selecting a disk.

### List virtual disks

```
list vdisk
```

Useful when working with VHD/VHDX files.



# `select`

Selects the object on which subsequent DiskPart commands operate.

### Select disk

```
select disk 1
```

### Select volume

```
select volume 3
```

### Select partition

```
select partition 2
```

### Select virtual disk

```
select vdisk file="C:\VMs\disk.vhdx"
```

Always verify your selection:

```
detail disk
```

or:

```
detail volume
```


# `detail`

Displays detailed information about the selected object.

### Disk

```
detail disk
```

### Volume

```
detail volume
```

### Partition

```
detail partition
```

### Virtual disk

```
detail vdisk
```


# `diskpart clean`

Erases partition information from the selected disk.

```
select disk 1
clean
```

This is **destructive**.

A safer learning workflow is simply:

```
list disk
select disk 1
detail disk
```

before performing any destructive operation.


# `diskpart create partition`

Creates partitions.

### Primary partition

```
create partition primary
```

Specify size in MB:

```
create partition primary size=10240
```

Creates approximately a 10 GB partition.

### Extended partition

On partitioning schemes where applicable:

```
create partition extended
```

### Logical partition

```
create partition logical
```


# `diskpart delete`

Deletes the selected partition or volume.

```
delete partition
```

or:

```
delete volume
```

This can destroy the data associated with that partition/volume.



# `assign`

Assigns a drive letter.

Example:

```
assign letter=Z
```

Remove a drive letter:

```
remove letter=Z
```

Example workflow:

```
select volume 3
assign letter=Z
```

Then from CMD:

```
Z:
```



# `format`

Formats the selected volume.

Example:

```
format fs=ntfs
```

Quick format:

```
format fs=ntfs quick
```

Specify a label:

```
format fs=ntfs label="LabDisk" quick
```

FAT32:

```
format fs=fat32 quick
```

exFAT:

```
format fs=exfat quick
```

Formatting destroys the existing filesystem data, so use a disposable lab volume.




# `extend`

Extends a volume into available unallocated space.

Example:

```
select volume 3
extend
```

Specify amount in MB:

```
extend size=5120
```

This attempts to extend the selected volume by approximately 5 GB.



# `shrink`

Shrinks a volume.

Example:

```
select volume 3
shrink
```

Specify amount:

```
shrink desired=5120
```

This attempts to free approximately 5 GB.



# `exit`

Leaves DiskPart.

```
exit
```



# Basic DiskPart Workflow

A safe inspection workflow:

```
diskpart
```

```
list disk
```

```
select disk 1
```

```
detail disk
```

```
list partition
```

```
list volume
```

Then exit:

```
exit
```

The important concept is:

```
Disk
 ↓
Partition
 ↓
Volume
 ↓
Filesystem
 ↓
Drive letter
```