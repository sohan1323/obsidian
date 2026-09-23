
---
Show files opened by a specific process:

```
lsof -p PID
```

Network connections:

```
lsof -p PID -i
```

This can help determine:

```
which files a process uses
which sockets it owns
which libraries/files it has open
```