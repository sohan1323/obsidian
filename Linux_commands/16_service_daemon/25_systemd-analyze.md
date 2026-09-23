
---
Analyzes systemd boot performance and dependencies.

### Boot time

```
systemd-analyze
```

Example:

```
Startup finished in 5.2s
```

### Slow services

```
systemd-analyze blame
```

Shows units ordered by startup time.

### Critical chain

```
systemd-analyze critical-chain
```

Shows dependencies contributing to boot delays.