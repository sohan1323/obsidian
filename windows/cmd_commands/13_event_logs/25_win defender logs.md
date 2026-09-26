
---
Find Defender-related channels:

```
wevtutil el | findstr /i "Defender"
```

You may find channels such as:

```
Microsoft-Windows-Windows Defender/Operational
```

Query:

```
wevtutil qe "Microsoft-Windows-Windows Defender/Operational" /c:20 /rd:true /f:text
```