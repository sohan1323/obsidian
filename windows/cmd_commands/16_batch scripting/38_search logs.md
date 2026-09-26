
---
```
@echo off

set "LOGDIR=C:\Lab\Logs"

if not exist "%LOGDIR%" (
    echo Log directory not found.
    exit /b 1
)

for /r "%LOGDIR%" %%F in (*.log) do (
    echo.
    echo ===== %%F =====
    findstr /i /n "error failed warning" "%%F"
)

exit /b 0
```

This combines:

```
if
for /r
variables
findstr
redirection
error handling
```