
---
The pipe sends one command's output into another command.

### Basic

```
command1 | command2
```

Example:

```
dir | more
```

Flow:

```
dir
 ↓
output
 ↓
more
```

### Find specific output

```
ipconfig /all | findstr /i "IPv4"
```

### Process filtering

```
tasklist | findstr /i "chrome"
```

### Network investigation

```
netstat -ano | findstr "LISTENING"
```

This pattern is extremely common in Windows administration and security.