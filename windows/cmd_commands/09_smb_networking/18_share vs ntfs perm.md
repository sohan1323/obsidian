
---
Suppose:

```
C:\Data
```

is shared as:

```
\\SERVER01\Data
```

There are two permission layers:

```
Network access
      ↓
SMB Share permissions
      ↓
NTFS permissions
      ↓
Actual access
```

Effective access is constrained by both layers.

For example, a user might have:

```
Share: Read
NTFS: Modify
```

Their network access cannot exceed the effective share restriction.