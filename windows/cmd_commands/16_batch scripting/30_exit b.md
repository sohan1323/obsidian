
---
Exit the current batch script or subroutine.

```
exit /b
```

Return a specific error code:

```
exit /b 0
```

Success:

```
exit /b 0
```

Failure:

```
exit /b 1
```

Example:

```
@echo off

if not exist "C:\Lab" (
    echo Lab directory missing.
    exit /b 1
)

echo Lab exists.
exit /b 0
```