
---
Gets the internal service name from a display name.

```
sc getkeyname "Print Spooler"
```

This is useful because commands such as:

```
sc query
sc stop
sc start
```

generally work with the **service name**, not the display name.