
---
Ends the localization started by `setlocal`.

```
endlocal
```

Typical structure:

```
@echo off

setlocal

set TEMP_VAR=Hello

echo %TEMP_VAR%

endlocal
```

This is important for writing batch scripts that don't accidentally modify the caller's environment.