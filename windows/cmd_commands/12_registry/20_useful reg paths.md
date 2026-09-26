
---
### Windows version

```
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion"
```

### Installed software

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall"
```

### Current user's software

```
reg query "HKCU\Software"
```

### Environment

```
reg query "HKCU\Environment"
```

Machine environment:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment"
```