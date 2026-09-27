
---
Displays information about system memory and memory blocks.

### Syntax

```
lsmem [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-a`|Show online and offline memory|
|`-b`|Show sizes in bytes|
|`-o`|Show memory block ranges|
|`-J`|JSON output|

### Examples

```
lsmem
```

Show all memory:

```
lsmem -a
```

### Practical use

Useful when investigating memory layout and hot-pluggable memory.