
---
```
timeout /t 5
```

Waits approximately 5 seconds.

Without allowing interruption:

```
timeout /t 5 /nobreak
```

Example:

```
echo Starting...
timeout /t 3 /nobreak >nul
echo Started.
```