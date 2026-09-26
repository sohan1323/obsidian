
---
Provides filesystem information.

### Drives

```
fsutil fsinfo drives
```

Example:

```
Drives: C:\ D:\ E:\
```

### Filesystem type

```
fsutil fsinfo volumeinfo C:
```

### NTFS information

```
fsutil fsinfo ntfsinfo C:
```

### Sector information

```
fsutil fsinfo sectorinfo C:
```

These are useful for low-level filesystem troubleshooting.