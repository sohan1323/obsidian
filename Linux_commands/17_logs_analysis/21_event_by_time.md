
---
With journal:

```
sudo journalctl -u ssh \
  --since "1 hour ago"
```

Failed authentication:

```
sudo journalctl -u ssh \
  --since "1 hour ago" |
  grep -i "failed"
```