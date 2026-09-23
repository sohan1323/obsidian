
---
Linux **capabilities** divide some root privileges into smaller privileges.

Find files with capabilities:

```
getcap -r / 2>/dev/null
```

Example:

```
/usr/bin/example cap_net_raw=ep
```

This means the executable has a specific capability rather than necessarily requiring full root privileges.