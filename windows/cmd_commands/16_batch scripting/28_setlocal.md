
---
Limits variable changes to the current batch script environment.

```
setlocal
set "TEMPVAR=hello"
echo %TEMPVAR%
endlocal

echo %TEMPVAR%
```

After `endlocal`, the variable created inside the local environment is normally unavailable.

Useful for preventing scripts from unnecessarily modifying the caller's environment.