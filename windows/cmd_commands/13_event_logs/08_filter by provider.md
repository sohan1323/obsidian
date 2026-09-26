
---
You can filter by event provider.

Example:

```
wevtutil qe System /q:"*[System[Provider[@Name='Service Control Manager']]]" /c:20 /rd:true
```

This can help investigate Windows service events.