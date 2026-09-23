
---
`perf` is a powerful Linux performance-analysis framework.

Check:

```
perf --version
```

Basic statistics:

```
perf stat command
```

Example:

```
perf stat ls
```

It can measure events such as:

```
CPU cycles
instructions
cache misses
branches
context switches
```


# `perf top`

Real-time performance profiling:

```
sudo perf top
```

It shows where CPU execution time is being spent.


# `perf record` and `perf report`

Record performance data:

```
perf record ./program
```

Analyze:

```
perf report
```

This is useful for advanced performance debugging.


# Advanced Process Investigation Workflow

```
Suspicious/slow process
        │
        ▼
      ps
        │
        ▼
     pgrep
        │
        ▼
     pstree
        │
        ▼
    /proc/PID
        │
   ┌────┼──────────┐
   ▼    ▼          ▼
cmdline environ    fd
   │    │          │
   └────┼──────────┘
        ▼
       lsof
        │
        ▼
     strace
        │
        ▼
     gdb/perf
```