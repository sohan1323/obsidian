
---
`watch` repeatedly executes a command at an interval.

```
watch command
```

Default interval is typically 2 seconds.

Example:

```
watch "date"
```

Another:

```
watch "ss -tuln"
```

Update every 5 seconds:

```
watch -n 5 "ss -tuln"
```

Useful for monitoring changing system state.

---

#  `watch` Options

|Option|Purpose|
|---|---|
|`-n SECONDS`|Set update interval|
|`-d`|Highlight differences|
|`-t`|Hide header|
|`-g`|Exit when output changes|

Example:

```
watch -n 1 -d "free -h"
```





# Scheduling Comparison

| Tool             | Use                                |
| ---------------- | ---------------------------------- |
| `cron`           | Recurring scheduled jobs           |
| `crontab`        | Manage cron jobs                   |
| `at`             | One-time scheduled command         |
| `atq`            | List `at` jobs                     |
| `atrm`           | Remove `at` job                    |
| `batch`          | Run when load is low               |
| `anacron`        | Periodic jobs that can catch up    |
| `systemd timers` | Modern service scheduling          |
| `sleep`          | Delay execution                    |
| `watch`          | Repeatedly execute/display command |