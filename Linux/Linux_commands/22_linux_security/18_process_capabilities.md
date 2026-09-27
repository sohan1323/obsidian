
---
Inspect a process:

```
cat /proc/PID/status
```

Look for:

```
CapInh
CapPrm
CapEff
CapBnd
CapAmb
```

Example:

```
grep '^Cap' /proc/$$/status
```

This displays the current shell's capability sets.