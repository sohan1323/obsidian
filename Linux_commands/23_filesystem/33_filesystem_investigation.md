
---


```
Filesystem problem
       │
       ▼
    findmnt
       │
       ▼
      df
       │
       ├── disk blocks → df -h
       │
       └── inodes → df -i
       │
       ▼
      du
       │
       ▼
  identify large files
       │
       ▼
      lsof
       │
       ▼
identify processes holding files
```

---


# Security-Relevant Filesystem Checks

### Find SUID files

```
find / -type f -perm -4000 2>/dev/null
```

### Find SGID files

```
find / -type f -perm -2000 2>/dev/null
```

### Find capabilities

```
getcap -r / 2>/dev/null
```

### Find writable files

```
find / -type f -writable 2>/dev/null
```

### Inspect mount security options

```
findmnt -o TARGET,SOURCE,FSTYPE,OPTIONS
```

Look for options such as:

```
nosuid
noexec
nodev
```

### Inspect suspicious symlinks

```
find /path -type l -ls
```