
---
Calls another batch file or a batch subroutine.

### Call another script

```
call backup.bat
```

### Pass arguments

```
call backup.bat C:\Data D:\Backup
```

### Batch subroutine

```
@echo off

call :hello

exit /b

:hello
echo Hello from subroutine
exit /b
```

`call :label` is useful for creating reusable functions in batch scripts.