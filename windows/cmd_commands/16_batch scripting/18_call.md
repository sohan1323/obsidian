
---
`call` can execute another batch file.

```
call script2.bat
```

It can also call a subroutine.

```
call :function
exit /b

:function
echo Inside function
exit /b
```

This is extremely useful for creating reusable batch functions.