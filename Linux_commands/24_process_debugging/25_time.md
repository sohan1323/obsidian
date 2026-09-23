
---
Measures how long a command takes.

```
time command
```

Example:

```
time find /etc -type f
```

Typical information:

```
real
user
sys
```

Meaning:

```
real → elapsed wall-clock time
user → CPU time in user space
sys  → CPU time in kernel space
```