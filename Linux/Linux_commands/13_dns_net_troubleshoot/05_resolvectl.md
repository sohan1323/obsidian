
---
particularly important for DNS troubleshooting.

### Show resolver configuration

```
resolvectl status
```

### Query hostname

```
resolvectl query example.com
```

### Show DNS servers

```
resolvectl dns
```

### Show DNS domains

```
resolvectl domain
```

### Flush DNS cache

On systems using `systemd-resolved`:

```
sudo resolvectl flush-caches
```