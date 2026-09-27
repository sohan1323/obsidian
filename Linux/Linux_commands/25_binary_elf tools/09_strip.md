
---
Removes symbols and debugging information from binaries.

### Syntax

```
strip [OPTIONS] FILE
```

Example:

```
strip program
```

Remove debug information:

```
strip --strip-debug program
```

Remove symbols:

```
strip --strip-all program
```

Keep debugging information:

```
strip --only-keep-debug program
```

### Why stripping matters

Before:

```
nm program
```

might show:

```
main
authenticate
check_password
```

After stripping:

```
nm program
```

may show:

```
no symbols
```

This makes reverse engineering more difficult, but **does not remove the machine code**.