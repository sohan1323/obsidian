
---
Checks whether a file or directory exists.

### Syntax

```
if exist filename command
```

Example:

```
if exist C:\Windows echo Windows exists
```

With `else`:

```
if exist config.txt (
    echo Configuration found
) else (
    echo Configuration missing
)
```

This is extremely common in batch scripts.