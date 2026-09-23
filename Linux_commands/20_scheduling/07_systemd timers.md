
---
Modern Linux systems commonly use **systemd timers** for scheduled tasks.

List timers:

```
systemctl list-timers
```

All timers:

```
systemctl list-timers --all
```

Example output:

```
NEXT                 LEFT       LAST
Wed 2026-09-23 12:00  10min      ...
```