
---
### Purpose

Displays RAM and swap memory usage.

### Syntax

```
free [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-h`|Human-readable|
|`-m`|Display in MB|
|`-g`|Display in GB|
|`-s SECONDS`|Repeat at interval|
|`-c COUNT`|Number of repetitions|
|`-t`|Show total RAM + swap|

### Examples

```
free -h
```

Example:

```
              total   used   free   shared   buff/cache   available
Mem:           16Gi    8Gi    2Gi      ...       6Gi          7Gi
Swap:           4Gi    0Gi    4Gi
```

Monitor every 2 seconds:

```
free -h -s 2
```

Run 5 times:

```
free -h -s 2 -c 5
```

### Practical use

Check whether a VM is running out of memory:

```
free -h
```