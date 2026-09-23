
---
Common pattern:

```
command > output.log 2>&1 &
```

Example:

```
python server.py > server.log 2>&1 &
```

Flow:

```
server.py
   ├── stdout → server.log
   └── stderr → server.log
             ↓
            &
       background
```