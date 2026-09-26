
---
`reg` can operate against another Windows computer when remote registry access and appropriate permissions are available.

General syntax:

```
reg query \\SERVER01\HKLM\SOFTWARE
```

Example:

```
reg query \\SERVER01\HKLM\SOFTWARE\Microsoft
```

Remote operations depend on:

- Network connectivity
- Authentication
- Permissions
- Remote Registry configuration
- Firewall/network policy