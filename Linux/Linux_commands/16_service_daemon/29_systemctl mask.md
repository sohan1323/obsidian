
---
Prevents a service from being started.

```
sudo systemctl mask nginx
```

A masked service cannot normally be started until unmasked.

Unmask:

```
sudo systemctl unmask nginx
```

### Difference

```
disable
    ↓
won't automatically start at boot

mask
    ↓
prevents the service from being started normally
```