
---
A systemd timer normally triggers a systemd service.

Conceptually:

```
timer
  │
  ▼
service
  │
  ▼
command/script
```

Example:

```
backup.timer
     ↓
backup.service
     ↓
/usr/local/bin/backup.sh
```


# Inspect a Timer

```
systemctl status backup.timer
```

View its configuration:

```
systemctl cat backup.timer
```

Check next execution:

```
systemctl list-timers backup.timer
```

