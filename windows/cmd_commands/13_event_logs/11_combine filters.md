
---
You can combine Event ID and provider.

Example:

```
wevtutil qe System /q:"*[System[(EventID=7045) and Provider[@Name='Service Control Manager']]]" /rd:true /c:20 /f:text
```

This is useful for investigating service-installation events where that event is logged.