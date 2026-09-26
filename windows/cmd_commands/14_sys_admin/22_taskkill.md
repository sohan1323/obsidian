
---
Terminate a process.

By image:

```
taskkill /im notepad.exe
```

By PID:

```
taskkill /pid 1234
```

Force:

```
taskkill /f /pid 1234
```

Include child processes:

```
taskkill /t /pid 1234
```

Force + tree:

```
taskkill /f /t /pid 1234
```

Use carefully.