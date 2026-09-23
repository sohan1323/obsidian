
---
Manages automatic log rotation.

### Configuration

Main configuration:

```
cat /etc/logrotate.conf
```

Additional configurations:

```
ls -la /etc/logrotate.d/
```

View a specific configuration:

```
cat /etc/logrotate.d/nginx
```

### Test configuration

```
sudo logrotate -d /etc/logrotate.conf
```

`-d` performs a debug/dry-run style operation without actually rotating.

### Force rotation

```
sudo logrotate -f /etc/logrotate.conf
```

Use carefully.

### Verbose

```
sudo logrotate -v /etc/logrotate.conf
```