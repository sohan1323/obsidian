
---
A common pattern:

```
@echo off

mkdir C:\Lab\Test

if errorlevel 1 (
    echo Failed to create directory.
    exit /b 1
)

echo Directory created successfully.
exit /b 0
```

Another pattern:

```
command

if %ERRORLEVEL% NEQ 0 (
    echo ERROR: Command failed.
    exit /b %ERRORLEVEL%
)
```