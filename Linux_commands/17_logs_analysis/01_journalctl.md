
---
Reads logs collected by **systemd-journald**.

### Syntax

```
journalctl [OPTIONS]
```

### View all logs

```
journalctl
```

### Latest logs

```
journalctl -n 50
```

### Follow logs live

```
journalctl -f
```

### Logs for a service

```
journalctl -u ssh
```

```
journalctl -u nginx
```

Follow:

```
journalctl -u ssh -f
```

### Current boot

```
journalctl -b
```

Previous boot:

```
journalctl -b -1
```

### Kernel logs

```
journalctl -k
```

### Logs since a time

```
journalctl --since "1 hour ago"
```

```
journalctl --since "2026-09-23 08:00:00"
```

Time range:

```
journalctl \
  --since "2026-09-23 08:00:00" \
  --until "2026-09-23 09:00:00"
```

### Priority

Errors:

```
journalctl -p err
```

Warnings and above:

```
journalctl -p warning
```

### Show logs for a process ID

```
journalctl _PID=1234
```

### Show logs for a user

```
journalctl _UID=1000
```

### Disk usage

```
journalctl --disk-usage
```

### Practical security use

Search authentication failures:

```
journalctl | grep -i "failed"
```

SSH logs:

```
journalctl -u ssh
```