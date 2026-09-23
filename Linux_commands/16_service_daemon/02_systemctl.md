
---
`systemctl` is the primary command for controlling **systemd** services and other systemd units.

### Syntax

```
systemctl [COMMAND] [UNIT]
```

---

## Check service status

```
systemctl status ssh
```

Example:

```
Active: active (running)
```

For nginx:

```
systemctl status nginx
```

### Practical use

Determine whether a service is:

- running
- stopped
- failed
- enabled
- disabled