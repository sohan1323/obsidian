
---
Displays or synchronizes system time with a network computer.

### Query a computer

```
net time \\SERVER01
```

Example:

```
net time \\192.168.1.20
```

---

## Query domain time

```
net time /domain
```

Synchronize time:

```
net time \\SERVER01 /set
```

The `/set` operation changes the local system time, so administrative privileges and appropriate permissions may be required.