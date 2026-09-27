
---
For an authorized system assessment, inspect:

### Process identity

```
ps -eo pid,ppid,user,group,comm
```

### Parent-child relationship

```
pstree -p
```

### Executable

```
readlink -f /proc/PID/exe
```

### Command line

```
tr '\0' ' ' < /proc/PID/cmdline
```

### Environment

```
sudo tr '\0' '\n' < /proc/PID/environ
```

### Open files

```
sudo lsof -p PID
```

### Network connections

```
sudo lsof -p PID -i
```

### Capabilities

```
grep '^Cap' /proc/PID/status
```

These provide a process-centric view:

```
Process
  │
  ├── identity
  ├── parent
  ├── executable
  ├── arguments
  ├── environment
  ├── files
  ├── sockets
  └── capabilities
```