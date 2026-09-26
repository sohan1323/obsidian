
---
For authorized security assessment, inspect:

### Task names

```
schtasks /query
```

### Detailed configuration

```
schtasks /query /fo list /v
```

### Specific task

```
schtasks /query /tn "\SomeTask" /fo list /v
```

Pay attention to:

- Action/command
- Executable path
- Arguments
- Run-as account
- Trigger
- Execution level
- Task permissions
- Whether referenced files/directories are writable