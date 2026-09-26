
---
`cl` = **Clear Log**

```
wevtutil cl Application
```

This clears the specified event log.

Security logs:

```
wevtutil cl Security
```

**Do not use this casually.** Clearing security logs destroys forensic evidence and generates its own security implications.

For authorized testing, use this only when explicitly required by the lab or administrative procedure.