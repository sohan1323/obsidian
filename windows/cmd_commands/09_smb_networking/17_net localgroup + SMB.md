
---
A useful administrative sequence is:

```
net view
```

Find a server:

```
\\SERVER01
```

Then:

```
net view \\SERVER01
```

You may find:

```
Share name
-----------
Public
Documents
Software
```

Then:

```
dir \\SERVER01\Public
```

Or:

```
net use Z: \\SERVER01\Public
```

Then:

```
Z:
dir
```

---

# 18. SMB Share Access Flow

Understand the complete relationship:

```
Windows Computer
       │
       ├── SMB Server
       │
       ├── Share
       │      └── C:\Shared
       │
       └── Network Client
                │
                └── \\SERVER\Share
```

For example:

```
SERVER01
   │
   └── Public
        │
        └── C:\Users\Public\Documents
```

The UNC path becomes:

```
\\SERVER01\Public
```