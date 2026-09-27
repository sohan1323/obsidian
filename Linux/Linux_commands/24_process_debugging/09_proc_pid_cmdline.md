
---
Shows the process command line:

```
cat /proc/PID/cmdline
```

Arguments are separated by NUL bytes.

Readable form:

```
tr '\0' ' ' < /proc/PID/cmdline
```