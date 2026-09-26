
---
A common user startup location is:

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Query:

```
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Run"
```

Machine-wide:

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
```

These locations are relevant to legitimate administration and security auditing because applications can configure themselves to launch when a user logs in.