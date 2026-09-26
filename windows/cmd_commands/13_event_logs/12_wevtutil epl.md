
---
`epl` = **Export Log**

Exports an event log to an `.evtx` file.

### Syntax

```
wevtutil epl LogName OutputFile
```

Example:

```
wevtutil epl System C:\Lab\System.evtx
```

Security log:

```
wevtutil epl Security C:\Lab\Security.evtx
```

This is useful for:

- Incident response
- Forensics
- Backup
- Offline analysis