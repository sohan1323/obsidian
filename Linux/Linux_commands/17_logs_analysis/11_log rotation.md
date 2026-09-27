
---
Logs can grow indefinitely, so Linux commonly uses **log rotation**.

Typical rotated files:

```
auth.log
auth.log.1
auth.log.2.gz
auth.log.3.gz
```

The general process is:

```
Current log
    ↓
Rotate
    ↓
Old log
    ↓
Compress
    ↓
Eventually delete
```