
---
Limits environment-variable changes to the current batch script/local scope.

```
setlocal
```

Example:

```
@echo off

setlocal
set TEST=Hello

echo %TEST%

endlocal

echo %TEST%
```

After `endlocal`, `TEST` is no longer available if it wasn't defined before the `setlocal`.