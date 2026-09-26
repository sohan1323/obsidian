
---
Exports a registry key to a `.reg` file.

### Syntax

```
reg export KeyName FileName
```

Example:

```
reg export HKCU\Software\LabTest C:\Lab\LabTest.reg
```

Force overwrite:

```
reg export HKCU\Software\LabTest C:\Lab\LabTest.reg /y
```

The resulting file can be opened as text and imported later.