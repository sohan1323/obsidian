
---
A directory can be mounted at another location.

```
sudo mount --bind /source /destination
```

Now both paths refer to the same underlying directory contents.

Remove:

```
sudo umount /destination
```

This is useful in system administration, containers, and filesystem isolation.