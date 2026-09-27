
---
Useful for understanding systemd calendar expressions.

Example:

```
systemd-analyze calendar daily
```

Or:

```
systemd-analyze calendar "Mon *-*-* 09:00:00"
```

It helps verify when a timer expression will trigger.