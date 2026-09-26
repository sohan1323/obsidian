
---
Recursive file processing.

### Syntax

```
for /r [path] %variable in (pattern) do command
```

Example:

```
for /r C:\Lab %f in (*.log) do echo %f
```

Finds `.log` files recursively.

This is similar in concept to:

```
dir /s *.log
```

but `for /r` allows you to **perform an operation on each matching file**.

Example:

```
for /r C:\Lab %f in (*.txt) do type "%f"
```