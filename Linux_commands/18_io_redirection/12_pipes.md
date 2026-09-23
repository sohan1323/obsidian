
---
A pipe sends stdout of one command to stdin of another.

```
command1 | command2
```

Example:

```
ls | grep ".txt"
```

Flow:

```
ls stdout
    ↓
   pipe
    ↓
grep stdin
```