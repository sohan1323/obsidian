
---
Windows commonly has hidden administrative shares such as:

```
C$
ADMIN$
IPC$
```

Example:

```
dir \\SERVER01\C$
```

Access requires appropriate administrative credentials.

`C$` represents the system drive.

These shares are important in Windows administration and security assessment because they provide remote administrative access when properly authorized.