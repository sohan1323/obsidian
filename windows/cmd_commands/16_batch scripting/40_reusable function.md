
---
```
@echo off

setlocal

call :CheckFile "C:\Lab\test.txt"
call :CheckFile "C:\Lab\data.txt"

exit /b 0


:CheckFile

if exist "%~1" (
    echo [FOUND] %~1
) else (
    echo [MISSING] %~1
)

exit /b
```

Here:

```
call :CheckFile
```

calls a subroutine.

```
%~1
```

is the function argument.