
---
**Purpose:** Change the niceness of an already running process.

### Syntax

```
renice PRIORITY [-p PID]
```

Example:

```
renice 10 -p 1234
```

Change process `1234` to niceness `10`.

By user:

```
sudo renice 10 -u alice
```

### Important

Increasing niceness makes a process more willing to yield CPU time.

Decreasing niceness gives it higher priority and generally requires elevated privileges.