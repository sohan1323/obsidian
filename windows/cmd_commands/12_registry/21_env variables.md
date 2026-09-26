
---
Query:

```
reg query HKCU\Environment
```

You may find values such as:

```
Path
TEMP
TMP
```

Machine-wide values:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment"
```

This is useful for understanding how Windows constructs the process environment.