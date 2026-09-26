
---
```
@echo off

setlocal

set "OUT=%~dp0system-info.txt"

echo Collecting system information...

(
    echo ==============================
    echo Windows System Information
    echo ==============================
    echo.
    echo Computer:
    hostname
    echo.
    echo Current User:
    whoami
    echo.
    echo OS Information:
    systeminfo
    echo.
    echo Network:
    ipconfig /all
    echo.
    echo Processes:
    tasklist
    echo.
    echo Listening Ports:
    netstat -ano
) > "%OUT%" 2>&1

echo.
echo Report saved to:
echo %OUT%

endlocal
```

This is a useful authorized-administration/security-lab pattern:

```
Collect
   ↓
Redirect
   ↓
Save
   ↓
Analyze
```