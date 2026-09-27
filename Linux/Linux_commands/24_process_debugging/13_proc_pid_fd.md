
---
Lists file descriptors opened by a process.

```
ls -l /proc/PID/fd
```

Example:

```
0 -> /dev/pts/0
1 -> /tmp/output.log
2 -> /tmp/error.log
```

Remember:

```
0 → stdin
1 → stdout
2 → stderr
```