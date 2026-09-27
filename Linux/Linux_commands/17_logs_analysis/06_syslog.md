
---
Common on Debian/Ubuntu systems.

View:

```
sudo less /var/log/syslog
```

Search errors:

```
sudo grep -i "error" /var/log/syslog
```

Follow:

```
sudo tail -f /var/log/syslog
```

### Purpose

May contain general system events such as:

- services
- networking
- applications
- system activity