
---
Reports system performance statistics related to:

- processes
- memory
- paging
- I/O
- CPU

### Syntax

```
vmstat [OPTION] [DELAY [COUNT]]
```

### Examples

```
vmstat
```

Monitor every 2 seconds:

```
vmstat 2
```

Run 5 times:

```
vmstat 2 5
```

Show memory statistics:

```
vmstat -s
```

### Important output fields

|Field|Meaning|
|---|---|
|`r`|Runnable processes|
|`b`|Processes blocked|
|`si`|Swap in|
|`so`|Swap out|
|`bi`|Blocks received|
|`bo`|Blocks sent|
|`us`|User CPU|
|`sy`|System CPU|
|`id`|Idle CPU|
|`wa`|I/O wait|

### Practical use

Identify resource pressure:

```
vmstat 1
```

High `wa` can indicate I/O waiting.

High `si`/`so` can indicate swapping.