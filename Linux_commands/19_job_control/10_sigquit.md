
---
Sends:

```
SIGQUIT
```

to the foreground process.

```
Ctrl+C  → SIGINT
Ctrl+Z  → SIGTSTP
Ctrl+\  → SIGQUIT
```

`SIGQUIT` normally terminates the process and may produce a core dump if configured.