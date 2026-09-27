
---
Displays detailed properties of a systemd unit.

```
systemctl show nginx
```

Specific property:

```
systemctl show nginx -p MainPID
```

Other useful properties:

```
systemctl show nginx -p User
```

```
systemctl show nginx -p ExecStart
```

### Practical use

Determine:

- service PID
- user running service
- executable
- dependencies
- environment
- restart behavior