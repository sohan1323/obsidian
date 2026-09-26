
---
For normal system enumeration:

### View drives

```
fsutil fsinfo drives
```

### View volume information

```
mountvol
```

### View filesystem

```
fsutil fsinfo volumeinfo C:
```

### View NTFS information

```
fsutil fsinfo ntfsinfo C:
```

### Check free space

```
fsutil volume diskfree C:
```

### Check filesystem

```
chkdsk C: /scan
```

### View volume label

```
vol C:
```