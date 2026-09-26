
---
Suppose you find a suspicious or simply interesting process:

```
tasklist | findstr /i "example"
```

Get its PID:

```
tasklist /fi "imagename eq example.exe"
```

Then inspect the process:

```
tasklist /fi "pid eq 1234" /v
```

And terminate it only when appropriate:

```
taskkill /pid 1234
```

Force termination:

```
taskkill /f /pid 1234
```