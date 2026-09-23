
---
Special device that discards data.

```
command > /dev/null
```

Discard stdout.

Discard stderr:

```
command 2> /dev/null
```

Discard both:

```
command > /dev/null 2>&1
```

Common example:

```
find / -name "*.conf" 2>/dev/null
```

Permission errors are discarded.