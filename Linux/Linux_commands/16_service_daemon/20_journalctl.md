
---
Reads logs collected by **systemd-journald**.

### Syntax

```
journalctl [OPTIONS]
```

---

## View all logs

```
journalctl
```

---

## Follow logs live

```
journalctl -f
```

Similar concept to:

```
tail -f
```

---

## Logs for a service

```
journalctl -u nginx
```

Follow:

```
journalctl -u nginx -f
```

---

## Logs from current boot

```
journalctl -b
```

Previous boot:

```
journalctl -b -1
```

---

## Show recent logs

```
journalctl -n 50
```

Last 100 lines:

```
journalctl -n 100
```

---

## Logs since a time

```
journalctl --since "1 hour ago"
```

Specific range:

```
journalctl --since "2026-09-23 08:00:00" --until "2026-09-23 09:00:00"
```

---

## Priority filtering

Errors:

```
journalctl -p err
```

Warnings and above:

```
journalctl -p warning
```