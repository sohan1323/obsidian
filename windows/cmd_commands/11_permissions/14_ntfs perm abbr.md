
---
The most important `icacls` permissions are:

```
F  = Full control
M  = Modify
RX = Read and execute
R  = Read
W  = Write
D  = Delete
```

Example:

```
icacls C:\Lab /grant Alice:M
```

means Alice gets **Modify**.