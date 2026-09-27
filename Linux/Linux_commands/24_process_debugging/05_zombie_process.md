
---
A zombie is a process that has finished execution but whose parent hasn't collected its exit status.

Find zombies:

```
ps -eo pid,ppid,stat,comm | grep ' Z'
```

Example:

```
1234  1000 Z  child
```

Conceptually:

```
Parent
  │
  └── Zombie
       │
       └── finished execution
```

A zombie doesn't continue executing normal user code.