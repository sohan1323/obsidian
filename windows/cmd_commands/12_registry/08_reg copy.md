
---
Copies a registry key and its contents.

### Syntax

```
reg copy SourceKey DestinationKey
```

Example:

```
reg copy HKCU\Software\LabTest HKCU\Software\LabTestBackup
```

Force:

```
reg copy HKCU\Software\LabTest HKCU\Software\LabTestBackup /f
```