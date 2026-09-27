
---
Collects and displays historical system performance statistics.

`sar` is part of the **sysstat** package.

It can monitor:

- CPU
- memory
- disk
- network
- processes
- system load

### Syntax

```
sar [OPTION] [INTERVAL] [COUNT]
```

### Important options

|Option|Purpose|
|---|---|
|`-u`|CPU utilization|
|`-r`|Memory utilization|
|`-d`|Disk activity|
|`-n DEV`|Network device statistics|
|`-q`|Load/run queue|
|`-b`|I/O statistics|
|`-P ALL`|Per-CPU statistics|

### Examples

CPU:

```
sar -u
```

Memory:

```
sar -r
```

Network:

```
sar -n DEV
```

Disk:

```
sar -d
```

Monitor CPU every 2 seconds, 5 times:

```
sar -u 2 5
```

Per-CPU statistics:

```
sar -P ALL 2 5
```

### Practical use

Monitor system performance over time:

```
sar -u 1 10
```