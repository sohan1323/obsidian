
---
Deletes a registry key or value.

### Delete a value

```
reg delete HKCU\Software\LabTest /v TestValue
```

Force deletion:

```
reg delete HKCU\Software\LabTest /v TestValue /f
```

### Delete an entire key

```
reg delete HKCU\Software\LabTest /f
```

Deleting a key recursively removes its subkeys and values.