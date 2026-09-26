
---
Deletes files.

### Syntax

```
del [options] file
```

### Basic

```
del test.txt
```

### Multiple files

```
del *.tmp
```

### `/F`

Force deletion of read-only files.

```
del /f readonly.txt
```

### `/Q`

Quiet mode.

```
del /q *.tmp
```

### `/S`

Delete matching files from the current directory and subdirectories.

```
del /s *.log
```

### `/A`

Delete files based on attributes.

```
del /a:h hidden.txt
```

### Combined

```
del /f /q /s *.tmp
```

This means:

```
/F → force
/Q → no confirmation
/S → recursive
*.tmp → target files
```

### ⚠️ Important

`del` is not the same as moving something to the Recycle Bin. Treat it as a destructive operation.