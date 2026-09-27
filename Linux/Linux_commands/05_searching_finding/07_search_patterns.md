
---
# Essential Search Patterns

### Find all files

```
find . -type f
```

### Find all directories

```
find . -type d
```

### Find `.log` files

```
find /var -type f -name "*.log"
```

### Find files larger than 1 GB

```
find / -type f -size +1G 2>/dev/null
```

### Find files modified today/within 24h

```
find . -type f -mtime -1
```

### Find SUID files

```
find / -type f -perm -4000 2>/dev/null
```

### Find SGID files

```
find / -type f -perm -2000 2>/dev/null
```

### Find writable files

```
find / -type f -writable 2>/dev/null
```

### Find world-writable files

```
find / -type f -perm -002 2>/dev/null
```

### Find files containing `password`

```
grep -R "password" /etc 2>/dev/null
```

### Find executable files

```
find . -type f -executable
```

### Find broken symbolic links

```
find . -xtype l
```