
---
Saves a registry hive to a file.

### Syntax

```
reg save KeyName FileName
```

Example:

```
reg save HKCU C:\Lab\HKCU.hiv
```

System hives may require administrative privileges.

Example:

```
reg save HKLM\SYSTEM C:\Lab\SYSTEM.hiv
```

This is especially relevant to backup and forensic workflows.