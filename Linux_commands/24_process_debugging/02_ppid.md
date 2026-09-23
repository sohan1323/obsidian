
---
Every process normally has a parent process.

```
ps -o pid,ppid,comm
```

Example:

```
PID   PPID  COMMAND
1000   900  bash
1200  1000  python
```

Meaning:

```
bash
 └── python
```
