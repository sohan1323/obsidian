
---
Manages NTFS filesystem compression.

### Check compression

```
compact
```

### Compress a file

```
compact /c C:\Lab\file.txt
```

### Decompress

```
compact /u C:\Lab\file.txt
```

### Recursive

```
compact /c /s:C:\Lab
```

### Force compression

```
compact /c /f C:\Lab\file.txt
```

Useful switches:

| Switch | Purpose                     |
| ------ | --------------------------- |
| `/c`   | Compress                    |
| `/u`   | Uncompress                  |
| `/s`   | Operate recursively         |
| `/f`   | Force compression           |
| `/a`   | Display hidden/system files |