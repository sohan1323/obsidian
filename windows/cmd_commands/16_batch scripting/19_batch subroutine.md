
---
Example:

```
@echo off

call :hello Sohan
call :hello Alice

exit /b

:hello
echo Hello %~1
exit /b
```

Output:

```
Hello Sohan
Hello Alice
```

Here:

```
%~1
```

means the first argument with surrounding quotes removed.