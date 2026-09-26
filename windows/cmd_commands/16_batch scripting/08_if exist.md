
---
Check whether a file or directory exists.

```
if exist C:\Lab\test.txt echo File exists
```

Directory:

```
if exist C:\Lab\ echo Directory exists
```

Example:

```
@echo off

if exist "C:\Lab" (
    echo Lab directory found.
) else (
    echo Lab directory does not exist.
)
```