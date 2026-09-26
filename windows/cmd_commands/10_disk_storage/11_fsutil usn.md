
---
NTFS maintains a **USN Journal** that records filesystem changes.

Query journal information:

```
fsutil usn queryjournal C:
```

This is useful for filesystem administration and forensic investigation.

It can help understand changes involving:

- File creation
- File deletion
- File modification
- Renaming