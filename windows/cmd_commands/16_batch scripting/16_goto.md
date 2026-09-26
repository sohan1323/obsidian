
---
Create a label:

```
:start
echo Hello
goto start
```

This creates an infinite loop.

Usually you combine it with a condition:

```
:start

set /p choice=Continue? 

if /i "%choice%"=="y" goto start

echo Finished.
```