
---
```
systemctl list-units --type=service
```

Only running services:

```
systemctl list-units --type=service --state=running
```

Failed services:

```
systemctl --failed
```

### Practical security use

Quickly identify failed services:

```
systemctl --failed
```