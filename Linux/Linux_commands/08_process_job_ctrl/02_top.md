
---
**Purpose:** Interactive real-time process monitoring.

### Syntax

```
top [OPTIONS]
```

Run:

```
top
```

You'll see information such as:

```
CPU usage
Memory usage
Load average
Running processes
Process IDs
Users
```

### Useful keys inside `top`

|Key|Action|
|---|---|
|`q`|Quit|
|`k`|Kill a process|
|`r`|Change process priority|
|`P`|Sort by CPU|
|`M`|Sort by memory|
|`N`|Sort by PID|
|`T`|Sort by CPU time|
|`1`|Show individual CPU cores|
|`h`|Help|

### Practical use

If your system is slow:

```
top
```

Then press:

```
M
```

to identify processes consuming significant memory.

Press:

```
P
```

to identify high CPU consumers.