
---
You can combine `wevtutil` with `findstr`.

Example:

```
wevtutil qe Security /c:100 /rd:true /f:text | findstr /i "4625"
```

Search for a username:

```
wevtutil qe Security /c:200 /rd:true /f:text | findstr /i "alice"
```

Search for an IP:

```
wevtutil qe Security /c:200 /rd:true /f:text | findstr /i "192.168.1.50"
```

This is less precise than XPath filtering but useful for quick investigation.