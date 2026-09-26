
---
Copies files.

### Syntax

```
copy [/D] [/V] [/N] [/Y | /-Y] [/Z] source destination
```

### Basic

```
copy file.txt backup.txt
```

### Copy to another directory

```
copy file.txt C:\Backup\
```

### Copy multiple files

```
copy *.txt C:\Backup\
```

### `/Y`

Suppress overwrite confirmation.

```
copy /y file.txt C:\Backup\
```

### `/-Y`

Ask before overwriting.

```
copy /-y file.txt C:\Backup\
```

### `/V`

Verify that files are written correctly.

```
copy /v file.txt C:\Backup\
```

### `/Z`

Copy in restartable mode.

```
copy /z largefile.iso D:\Backup\
```

Useful for unstable network connections.