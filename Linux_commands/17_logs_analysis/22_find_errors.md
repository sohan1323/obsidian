
---
```
sudo grep -RniE "error|failed|denied" /var/log/ 2>/dev/null
```

Breakdown:

```
-R       recursive
-n       line number
-i       case-insensitive
-E       extended regex
```