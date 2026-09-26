
---
Syntax:

```
if errorlevel N command
```

Example:

```
somecommand

if errorlevel 1 (
    echo Command failed.
)
```

Important behavior:

```
if errorlevel 1
```

means **errorlevel >= 1**, not exactly `1`.

For exact comparison:

```
if %ERRORLEVEL% EQU 1 echo Error code is 1
```