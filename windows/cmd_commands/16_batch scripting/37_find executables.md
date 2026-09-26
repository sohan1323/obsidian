
---
```
@echo off

for %%P in (python.exe powershell.exe cmd.exe ssh.exe curl.exe) do (
    echo.
    echo ===== %%P =====
    where %%P
)

pause
```

Useful for checking which tools are installed and where they are located.