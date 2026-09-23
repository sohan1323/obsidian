
---
Converts an address into a source-code location when debugging information is available.

### Syntax

```
addr2line [OPTIONS] ADDRESS
```

Example:

```
addr2line -e ./program 0x401136
```

Typical output:

```
main.c:25
```

### Important option

```
-e FILE
```

Specifies executable.

Demangle C++:

```
addr2line -C -e ./program 0x401136
```

Useful when analyzing:

```
crashes
stack traces
core dumps
debugging information
```