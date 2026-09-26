
---
Tests a command's exit status.

```
if errorlevel 1 echo Command failed
```

A subtle point: `if errorlevel N` is true when the error level is **N or greater**, not only when it equals N.

For exact comparisons, you can use:

```
if %ERRORLEVEL% EQU 0 echo Success
```

or:

```
if %ERRORLEVEL% NEQ 0 echo Failure
```