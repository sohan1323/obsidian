
---
Persist an environment variable for future processes.

```
setx TEST "hello"
```

Then open a **new CMD window**:

```
echo %TEST%
```

Important distinction:

```
set
 ↓
Current CMD process

setx
 ↓
Future processes
```

Don't use `setx` to repeatedly modify `PATH` without understanding the consequences; careless use can overwrite or corrupt a user's PATH configuration.