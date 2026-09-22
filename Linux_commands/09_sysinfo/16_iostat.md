
---
Reports CPU and disk I/O statistics.

It is provided by the **sysstat** package on many distributions.

### Syntax

```
iostat [OPTION] [INTERVAL [COUNT]]
```

### Important options

|Option|Purpose|
|---|---|
|`-x`|Extended statistics|
|`-d`|Device statistics only|
|`-c`|CPU statistics only|
|`-h`|Human-readable|
|`-m`|MB/s|
|`-k`|KB/s|

### Examples

```
iostat
```

Disk statistics:

```
iostat -d
```

Detailed disk statistics:

```
iostat -x
```

Monitor every 2 seconds:

```
iostat -x 2
```

### Practical use

Identify disk bottlenecks:

```
iostat -xz 1
```

Important fields include:

- `%util`
- `await`
- read/write throughput
- IOPS