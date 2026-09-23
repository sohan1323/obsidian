
---
A core dump contains information about a process at the time it crashes.

Check core-dump limit:

```
ulimit -c
```

Unlimited:

```
ulimit -c unlimited
```

On systemd systems, core dumps can often be inspected with:

```
coredumpctl
```