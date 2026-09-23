
---
Monitor virtual memory/system activity:

```
vmstat
```

Repeated:

```
vmstat 2
```

Five samples:

```
vmstat 2 5
```

Useful fields:

```
r  → runnable processes
b  → blocked processes
si → swap in
so → swap out
bi → blocks in
bo → blocks out
us → user CPU
sy → system CPU
id → idle CPU
wa → I/O wait
```