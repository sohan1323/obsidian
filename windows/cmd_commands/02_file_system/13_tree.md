
---
Displays a directory structure.

### Syntax

```
tree [path] [/F] [/A]
```

### Basic

```
tree
```

Example:

```
C:.
├── Documents
├── Downloads
└── Projects
```

### `/F`

Display files as well.

```
tree /f
```

### `/A`

Use ASCII characters.

```
tree /a
```

Useful when redirecting output to a text file:

```
tree /f /a > structure.txt
```