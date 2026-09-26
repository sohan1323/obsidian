
---
# `set /p`

Gets input from the user.

```
set /p name=Enter your name: 
echo Hello %name%
```

Example:

```
@echo off

set /p filename=Enter filename: 

if exist "%filename%" (
    echo File exists.
) else (
    echo File not found.
)
```

This is useful for interactive scripts.