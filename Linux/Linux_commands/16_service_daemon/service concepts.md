
---
```
systemd
   │
   ├── service units (.service)
   ├── socket units (.socket)
   ├── timer units (.timer)
   ├── mount units (.mount)
   └── target units (.target)
```

A typical service lifecycle:

```
Installed
   ↓
Disabled
   ↓
Enable
   ↓
Start
   ↓
Running
   ↓
Stop / Restart
```