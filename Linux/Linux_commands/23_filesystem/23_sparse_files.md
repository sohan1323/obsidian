
---
A sparse file has a large logical size but doesn't necessarily consume equivalent physical disk space.

Create one:

```
truncate -s 1G sparse.img
```

Check apparent size:

```
ls -lh sparse.img
```

Check actual disk usage:

```
du -h sparse.img
```

These values can differ significantly.