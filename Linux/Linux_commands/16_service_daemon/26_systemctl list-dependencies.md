
---
Shows dependencies of a systemd unit.

```
systemctl list-dependencies nginx
```

Reverse dependencies:

```
systemctl list-dependencies --reverse nginx
```

### Practical use

Understand what services a service depends on.