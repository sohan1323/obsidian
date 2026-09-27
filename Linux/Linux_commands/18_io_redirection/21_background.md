
---
Run a command asynchronously.

```
command &
```

Example:

```
sleep 30 &
```

Bash immediately returns control to the terminal.

You can inspect it with:

```
jobs
```

Job control was covered separately, so the important point here is that `&` creates asynchronous execution.