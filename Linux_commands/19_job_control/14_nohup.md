
---
Normally, a process associated with your terminal may receive `SIGHUP` when the terminal/session closes.

`nohup` helps keep a command running after logout.

```
nohup command &
```

Example:

```
nohup python server.py &
```

By default, output may be written to:

```
nohup.out
```

Better:

```
nohup python server.py > server.log 2>&1 &
```

Now:

```
stdout → server.log
stderr → server.log
process → background
```