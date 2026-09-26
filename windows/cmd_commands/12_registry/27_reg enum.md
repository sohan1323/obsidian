
---
For an authorized security assessment, useful queries include:

### OS information

```
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion"
```

### Installed software

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" /s
```

### Startup entries

```
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Run"
```

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
```

### Services

```
reg query "HKLM\SYSTEM\CurrentControlSet\Services" /s
```

### Environment

```
reg query "HKCU\Environment"
```

These queries are useful for understanding system configuration during authorized assessment.

# `reg query` + `findstr`

Registry output can be filtered using the CMD pipeline.

Example:

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" /s | findstr /i "DisplayName"
```

Search for a particular application:

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" /s | findstr /i "python"
```

Search service configurations:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Services" /s | findstr /i "ImagePath"
```


# Registry Backup Workflow

For a lab registry key:

```
reg export HKCU\Software\LabTest C:\Lab\LabTest.reg /y
```

Make changes:

```
reg add HKCU\Software\LabTest /v TestValue /t REG_SZ /d "Changed"
```

Verify:

```
reg query HKCU\Software\LabTest
```

Restore:

```
reg import C:\Lab\LabTest.reg
```

Verify:

```
reg query HKCU\Software\LabTest
```