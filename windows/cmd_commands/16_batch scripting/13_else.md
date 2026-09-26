
---
```
if exist "C:\Lab" (
    echo Exists
) else (
    echo Missing
)
```

Important: in batch syntax, `else` normally needs to be on the same logical line as the closing `)`:

```
) else (
```