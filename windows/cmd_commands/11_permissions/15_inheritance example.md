
---
Suppose:

```
C:\Lab
 ├── report.txt
 └── Documents
      └── notes.txt
```

You execute:

```
icacls C:\Lab /grant Alice:(OI)(CI)M
```

Conceptually:

```
C:\Lab
   │
   ├── report.txt
   │      ↑
   │      OI
   │
   └── Documents
          ↑
          CI
          │
          └── notes.txt
```

`OI` allows inheritance to objects/files.

`CI` allows inheritance to containers/directories.