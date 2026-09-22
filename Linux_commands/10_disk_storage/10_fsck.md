
---
Checks and repairs filesystems.

### Syntax

```
sudo fsck [OPTION] DEVICE
```

### Important options

|Option|Purpose|
|---|---|
|`-f`|Force filesystem check|
|`-y`|Automatically answer yes|
|`-n`|Do not make changes|
|`-V`|Verbose|

### Examples

Check a filesystem without modifying it:

```
sudo fsck -n /dev/sdb1
```

Force a check:

```
sudo fsck -f /dev/sdb1
```

### Important

Do **not** normally run `fsck` against a mounted writable filesystem.

For example, avoid:

```
sudo fsck /dev/sda2
```

if `/dev/sda2` is your currently mounted root filesystem.