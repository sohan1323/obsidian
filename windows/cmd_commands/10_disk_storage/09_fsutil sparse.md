
---
Sparse files allow files to consume less physical storage than their logical size.

### Query

```
fsutil sparse queryflag C:\test.img
```

### Set sparse attribute

```
fsutil sparse setflag C:\test.img
```

Sparse files are useful with:

- Virtual disks
- Databases
- Large files
- VM/storage systems