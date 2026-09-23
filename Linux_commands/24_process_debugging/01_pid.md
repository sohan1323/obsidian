
---
Every running process has a **PID**.

Find your shell PID:

```
echo $$
```

Find a process:

```
pgrep nginx
```

Inspect:

```
ps -p PID -f
```