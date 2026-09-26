
---
Provides predefined choices.

Syntax:

```
choice /c choices /m "message"
```

Example:

```
choice /c YN /m "Continue?"
```

The user sees:

```
Continue? [Y,N]?
```

Result is stored in `ERRORLEVEL`.

```
choice /c YN /m "Continue?"

if errorlevel 2 goto no
if errorlevel 1 goto yes

:yes
echo Yes
goto end

:no
echo No

:end
```

Important: test higher choice numbers first.