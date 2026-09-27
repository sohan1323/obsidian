
---
Displays and manages **MBR/GPT partition tables**.

### Syntax

```
sudo fdisk [OPTION] DEVICE
```

### Important options

|Option|Purpose|
|---|---|
|`-l`|List partition tables|
|`-u`|Display sectors instead of cylinders on older fdisk versions|
|`-s`|Display partition size in blocks|

### Examples

List all disks:

```
sudo fdisk -l
```

Inspect a disk:

```
sudo fdisk /dev/sdb
```

Inside the interactive interface:

|Command|Purpose|
|---|---|
|`p`|Print partition table|
|`n`|Create partition|
|`d`|Delete partition|
|`t`|Change partition type|
|`w`|Write changes|
|`q`|Quit without saving|
|`m`|Help|

### Important

`fdisk` can modify partition tables.

Always verify the target device before performing destructive operations.