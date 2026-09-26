
---
Windows event levels commonly include:

```
1 = Critical
2 = Error
3 = Warning
4 = Information
5 = Verbose
```

Example:

```
wevtutil qe System /q:"*[System[Level=2]]" /c:20 /rd:true /f:text
```

This retrieves recent error-level events.