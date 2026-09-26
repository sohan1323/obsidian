
---
A scheduled task has several important security properties:

```
Task
 │
 ├── Trigger
 │
 ├── Action
 │
 ├── Run-as account
 │
 ├── Execution level
 │
 └── Permissions
```

Example:

```
Task: DailyBackup
Trigger: 02:00
Action: backup.exe
User: SYSTEM
Level: Highest
```

This matters because the **run-as account determines the security context in which the task executes**.