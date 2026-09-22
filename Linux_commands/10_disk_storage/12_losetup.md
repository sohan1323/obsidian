
---
Manages **loop devices**.

Loop devices allow files to be used as block devices.

### Syntax

```
losetup [OPTION] [DEVICE]
```

### Examples

List loop devices:

```
losetup -a
```

Attach an image:

```
sudo losetup /dev/loop0 disk.img
```

Detach:

```
sudo losetup -d /dev/loop0
```

Automatically find a free loop device:

```
sudo losetup -f disk.img
```

### Practical use

Disk-image analysis:

```
sudo losetup -f disk.img
```

Commonly useful in forensic and security work.