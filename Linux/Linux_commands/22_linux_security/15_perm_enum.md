
---
World-writable files:

```
find / -type f -perm -002 2>/dev/null
```

World-writable directories:

```
find / -type d -perm -002 2>/dev/null
```

SUID:

```
find / -type f -perm -4000 2>/dev/null
```

SGID:

```
find / -type f -perm -2000 2>/dev/null
```

Writable files:

```
find / -type f -writable 2>/dev/null
```

These commands are useful for authorized Linux security assessment.