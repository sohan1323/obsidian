
---
A simple lab enumeration script:

```
@echo off

setlocal

echo ==============================
echo Windows Lab Enumeration
echo ==============================

echo.
echo [1] Host
hostname

echo.
echo [2] User
whoami /all

echo.
echo [3] OS
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"

echo.
echo [4] Network
ipconfig /all

echo.
echo [5] Listening Ports
netstat -ano | findstr "LISTENING"

echo.
echo [6] Processes
tasklist

echo.
echo [7] Services
sc query type= service state= all

echo.
echo [8] Shares
net share

echo.
echo Enumeration complete.

endlocal
```

This is appropriate for your **own Windows VM/lab** and gives you a practical way to connect the commands you've learned.