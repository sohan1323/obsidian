
---
Controls CPU affinity.

Check current affinity:

```
taskset -p PID
```

Run a command on CPU 0:

```
taskset -c 0 command
```

Run on CPUs 0 and 1:

```
taskset -c 0,1 command
```

This is useful when investigating CPU scheduling and performance.