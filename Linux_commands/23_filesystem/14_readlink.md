
---
Display symbolic-link target:

```
readlink symlink.txt
```

Resolve the complete path:

```
readlink -f symlink.txt
```

Useful for determining where a symlink ultimately points.