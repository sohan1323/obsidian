
---
Provides advanced file operations.

For example:

```
fsutil file queryextents C:\test.txt
```

This queries the physical extents associated with a file.

Another useful operation is:

```
fsutil file seteof C:\test.txt 1000
```

This changes the end-of-file position.

Because `fsutil file` can directly manipulate filesystem structures, avoid experimenting on important files.