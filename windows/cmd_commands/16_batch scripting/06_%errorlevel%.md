
---
Many Windows commands return an exit status.

```
somecommand
echo %ERRORLEVEL%
```

Common convention:

```
0 = success
non-zero = error/failure
```

Example:

```
ping 127.0.0.1 >nul

echo ErrorLevel: %ERRORLEVEL%
```

You can use it for error handling:

```
command
if %ERRORLEVEL% NEQ 0 (
    echo Command failed.
)
```