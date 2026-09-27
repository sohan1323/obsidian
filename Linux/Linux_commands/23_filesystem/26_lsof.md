
---
Lists open files.

```
lsof
```

Find processes using a file:

```
lsof /var/log/syslog
```

Find network sockets:

```
sudo lsof -i
```

Specific port:

```
sudo lsof -i :22
```

This is useful for determining which process owns a resource.