
---
### Purpose

Displays basic information about the Linux kernel and operating system.

### Syntax

```
uname [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-a`|Show all available information|
|`-s`|Kernel name|
|`-r`|Kernel release/version|
|`-v`|Kernel version/build information|
|`-m`|Machine hardware architecture|
|`-p`|Processor type|
|`-i`|Hardware platform|
|`-o`|Operating system|

### Examples

```
uname
```

```
Linux
```

```
uname -r
```

Shows kernel release:

```
6.8.0-xx-generic
```

```
uname -m
```

Shows architecture:

```
x86_64
```

```
uname -a
```

Shows all major information.

### Practical use

```
uname -r
```

Useful when checking the running kernel version during system enumeration.