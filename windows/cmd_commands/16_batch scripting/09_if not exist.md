
---
```
if not exist "C:\Lab" mkdir "C:\Lab"
```

Example:

```
@echo off

if not exist "C:\Lab" (
    mkdir "C:\Lab"
    echo Created C:\Lab
)
```