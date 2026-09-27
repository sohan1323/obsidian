
---
# Log Analysis Pipeline

```
grep "Failed password" /var/log/auth.log \
    | awk '{print $11}' \
    | sort \
    | uniq -c \
    | sort -nr
```

Flow:

```
auth.log
   ↓
grep
   ↓
awk
   ↓
sort
   ↓
uniq -c
   ↓
sort -nr
```

This is a typical Linux command-line pipeline.



# Error Capture

```
find / -name "*.conf" \
    > results.txt \
    2> errors.txt
```

You get:

```
results.txt → successful results
errors.txt  → permission/errors
```



# Complete Capture

```
find / -name "*.conf" > results.txt 2>&1
```

Everything goes to:

```
results.txt
```

Or:

```
find / -name "*.conf" &> results.txt
```





# Stream Diagram

```
                ┌──────────────┐
Keyboard ─────→ │ stdin   (0)  │
                │              │
                │   COMMAND    │
                │              │
Terminal ←───── │ stdout  (1)  │
                │              │
Terminal ←───── │ stderr  (2)  │
                └──────────────┘
```

With a pipe:

```
COMMAND 1
stdout (1)
     │
     ▼
    PIPE
     │
     ▼
COMMAND 2
stdin (0)
```