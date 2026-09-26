
---
Controls filesystem behavior.

Query a setting:

```
fsutil behavior query DisableDeleteNotify
```

This is commonly used to inspect TRIM-related behavior.

For example:

```
NTFS DisableDeleteNotify = 0
```

generally indicates that TRIM notifications are enabled for NTFS.