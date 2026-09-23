
---
A hard link is another directory entry referring to the same inode.

Create:

```
ln original.txt hardlink.txt
```

Check:

```
ls -li original.txt hardlink.txt
```

You will see the same inode number.

Conceptually:

```
original.txt ──┐
               ├── inode ── data
hardlink.txt ──┘
```

Deleting one name does not necessarily delete the underlying data.