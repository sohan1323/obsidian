
---
Create:

```
system-info.bat
```

with:

```
@echo off

setlocal

echo ==============================
echo       SYSTEM INFORMATION
echo ==============================

echo User       : %USERNAME%
echo Computer   : %COMPUTERNAME%
echo Directory  : %CD%
echo Windows    : %WINDIR%
echo Date       : %DATE%
echo Time       : %TIME%

echo.
echo Network:
ipconfig | findstr /i "IPv4"

echo.
echo Current User:
whoami

echo.
echo Processes:
tasklist | findstr /i "explorer"

echo.
pause

endlocal
```

Run:

```
system-info.bat
```

This combines:

- variables
- `echo`
- pipes
- `findstr`
- commands
- comments
- `setlocal`
- `pause`





# File Processing

```
@echo off

setlocal

set "SOURCE=C:\CLI-Lab"
set "DEST=C:\CLI-Lab\Backup"

if not exist "%DEST%" (
    mkdir "%DEST%"
)

for /r "%SOURCE%" %%F in (*.txt) do (
    echo Found: %%F
)

endlocal
```

Important concepts here:

```
set
if
exist
mkdir
for /r
variables
quoted paths
%%F
```