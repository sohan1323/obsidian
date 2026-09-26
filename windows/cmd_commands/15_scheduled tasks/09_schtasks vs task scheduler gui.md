
---
The GUI is:

```
Task Scheduler
```

The CLI is:

```
schtasks
```

Conceptually:

```
Task
 ├── Trigger
 ├── Action
 ├── Conditions
 ├── Settings
 ├── Security context
 └── History
```

`schtasks` exposes a significant portion of this functionality from the command line.