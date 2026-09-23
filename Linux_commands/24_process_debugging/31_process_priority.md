
---
Linux processes have a **nice value**.

Check:

```
ps -eo pid,ni,comm
```

Typical range:

```
-20 → highest priority
  0 → default
+19 → lowest priority
```


# `nice`

Start a command with a specified nice value:

```
nice -n 10 command
```

Higher nice value generally means lower CPU scheduling priority.

Example:

```
nice -n 15 ./heavy-task
```



# `renice`

Change priority of an existing process:

```
renice 10 -p PID
```

Check:

```
ps -o pid,ni,comm -p PID
```

Increasing priority with negative nice values normally requires elevated privileges.