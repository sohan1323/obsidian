
---
Sends a signal to processes belonging to a systemd service.

```
sudo systemctl kill nginx
```

Specific signal:

```
sudo systemctl kill -s SIGTERM nginx
```

Force:

```
sudo systemctl kill -s SIGKILL nginx
```

Normally, prefer proper service management:

```
sudo systemctl stop nginx
```

rather than manually killing service processes.