
---
Despite its name, `cipher` is primarily used for **NTFS EFS encryption management** and secure wiping of unused disk space.

### Display EFS information

```
cipher
```

### Encrypt a file

```
cipher /e C:\Lab\secret.txt
```

### Decrypt

```
cipher /d C:\Lab\secret.txt
```

### Recursive encryption

```
cipher /e /s:C:\Lab
```

### Show encryption state

```
cipher /c C:\Lab\secret.txt
```

### Wipe unused disk space

```
cipher /w:C:
```

`/w` operates on free space and can take significant time.