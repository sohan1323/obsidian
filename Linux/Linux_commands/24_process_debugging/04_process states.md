
---
View process state:

```
ps -eo pid,ppid,stat,comm
```

Common states:

|State|Meaning|
|---|---|
|`R`|Running/runnable|
|`S`|Interruptible sleep|
|`D`|Uninterruptible sleep|
|`T`|Stopped|
|`Z`|Zombie|
|`I`|Idle kernel thread|

Additional state characters may indicate properties such as multithreading or session leadership.