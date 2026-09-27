
---
Bash assigns jobs numbers:

```
[1]
[2]
[3]
```

You can reference a job using:

```
%1
%2
```

Example:

```
fg %1
```

means bring job 1 to the foreground.