
---
```
find / -type f -size +1G 2>/dev/null
```

Human-readable output:

```
find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null
```

Useful during disk-space investigations.



# Finding Recently Modified Files

Last 24 hours:

```
find /path -type f -mtime -1
```

Last hour:

```
find /path -type f -mmin -60
```

Useful when investigating unexpected filesystem changes.