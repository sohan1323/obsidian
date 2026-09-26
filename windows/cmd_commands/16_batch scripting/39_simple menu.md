
---
```
@echo off

:menu

cls

echo ==============================
echo       Windows CLI Lab
echo ==============================
echo.
echo 1. System Information
echo 2. Network Information
echo 3. Process List
echo 4. Exit
echo.

choice /c 1234 /m "Select an option"

if errorlevel 4 goto exit
if errorlevel 3 goto processes
if errorlevel 2 goto network
if errorlevel 1 goto system

:system
cls
systeminfo
pause
goto menu

:network
cls
ipconfig /all
pause
goto menu

:processes
cls
tasklist
pause
goto menu

:exit
echo Exiting...
exit /b 0
```

This demonstrates a fundamental pattern for building menu-driven Windows CLI utilities.