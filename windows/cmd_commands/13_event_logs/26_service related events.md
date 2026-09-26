
---
Find Service Control Manager events:

```
wevtutil qe System /q:"*[System[Provider[@Name='Service Control Manager']]]" /c:20 /rd:true /f:text
```

This can help investigate:

- Service starts
- Service stops
- Service failures
- Service configuration problems