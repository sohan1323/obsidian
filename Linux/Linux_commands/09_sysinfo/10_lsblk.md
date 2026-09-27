
---
Lists block devices such as:

- HDDs
- SSDs
- NVMe drives
- partitions
- LVM volumes

### Syntax

```
lsblk [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-f`|Show filesystem information|
|`-o`|Select columns|
|`-p`|Show full device paths|
|`-a`|Show all devices|
|`-t`|Show topology information|
|`-J`|JSON output|

### Examples

```
lsblk
```

Typical:

```
NAME        SIZE TYPE
sda         100G disk
├─sda1       1G part
└─sda2      99G part
```

Show filesystem information:

```
lsblk -f
```

Show full paths:

```
lsblk -p
```

Select columns:

```
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
```

### Practical use

Very important for disk enumeration:

```
lsblk -f
```

It can reveal:

- partitions
- filesystems
- mount points
- LVM volumes
- encrypted volumes