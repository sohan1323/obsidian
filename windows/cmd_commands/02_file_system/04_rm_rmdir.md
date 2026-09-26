
---
Deletes directories.

### Syntax

```
rmdir [/s] [/q] [drive:]path
```

### Delete empty directory

```
rmdir test
```

### `/S`

Deletes the directory and everything inside it.

```
rmdir /s test
```

CMD asks for confirmation.

### `/Q`

Quiet mode.

```
rmdir /s /q test
```

Deletes the directory tree without asking for confirmation.

### ⚠️ Important

This can permanently delete a large directory tree.

For example:

```
rmdir /s /q C:\Lab
```

removes `C:\Lab` and its contents.