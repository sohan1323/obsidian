
---
Common uninstall locations:

```
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall"
```

On 64-bit Windows, 32-bit applications may appear under:

```
reg query "HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall"
```

User-specific installations can also appear under HKCU.