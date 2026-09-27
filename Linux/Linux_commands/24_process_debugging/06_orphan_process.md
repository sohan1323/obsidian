
---
An orphan is a process whose original parent terminates before the child.

The process is adopted by another process, traditionally PID 1 or the system's service manager.

Inspect parent:

```
ps -o pid,ppid,comm -p PID
```