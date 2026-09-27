
---
Start:

```
sleep 100
```

Press:

```
Ctrl+Z
```

Now:

```
jobs
```

shows:

```
[1]+  Stopped    sleep 100
```

Resume in background:

```
bg %1
```

Check:

```
jobs
```

Bring it back:

```
fg %1
```

Terminate:

```
Ctrl+C
```