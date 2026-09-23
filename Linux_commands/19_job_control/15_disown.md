
---
Bash can remove a job from its job table.

Start:

```
sleep 1000 &
```

Check:

```
jobs
```

Then:

```
disown %1
```

The shell no longer manages that job as one of its jobs.

Useful when you want a process to remain independent of the shell.

### Common form

```
disown -h %1
```

This removes the job's susceptibility to `SIGHUP` while retaining it in the job table.