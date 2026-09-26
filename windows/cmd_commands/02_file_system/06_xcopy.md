
---
`xcopy` is an older, more capable copying command than `copy`.

It can copy directory structures.

### Syntax

```
xcopy source [destination] [options]
```

### Basic

```
xcopy C:\Projects D:\Backup
```

### `/E`

Copy directories, including empty directories.

```
xcopy C:\Projects D:\Backup /e
```

### `/S`

Copy directories except empty ones.

```
xcopy C:\Projects D:\Backup /s
```

### `/I`

Assume destination is a directory.

```
xcopy *.txt D:\Backup /i
```

### `/H`

Include hidden and system files.

```
xcopy C:\Data D:\Backup /e /h
```

### `/Y`

Suppress overwrite prompts.

```
xcopy C:\Data D:\Backup /e /y
```

### `/D`

Copy files newer than the destination.

```
xcopy C:\Data D:\Backup /d
```

### `/C`

Continue despite errors.

```
xcopy C:\Data D:\Backup /c
```

### `/R`

Overwrite read-only files.

```
xcopy C:\Data D:\Backup /r
```

### `/K`

Preserve file attributes.

```
xcopy C:\Data D:\Backup /k
```

### `/X`

Copy file audit settings.

Useful when preserving NTFS security information.