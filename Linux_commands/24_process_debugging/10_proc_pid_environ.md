
---
Shows the process environment.

```
sudo tr '\0' '\n' < /proc/PID/environ
```

This can reveal environment variables available to the process.

Be careful: applications may contain sensitive values such as tokens or credentials in their environment.