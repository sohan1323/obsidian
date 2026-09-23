
---
```
sudo systemctl reload nginx
```

Reloads configuration without fully stopping the service, if that service supports reload.

### Difference

```
restart
    ↓
stop + start

reload
    ↓
reload configuration while keeping service running
```