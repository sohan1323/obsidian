
---
PowerShell can produce its own operational events.

First locate the channel:

```
wevtutil el | findstr /i "PowerShell"
```

Common channel:

```
Microsoft-Windows-PowerShell/Operational
```

Query it:

```
wevtutil qe Microsoft-Windows-PowerShell/Operational /c:20 /rd:true /f:text
```

This can be useful during PowerShell troubleshooting and authorized security investigations.