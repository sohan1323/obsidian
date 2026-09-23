
---
A command's output can be connected to another command.

Example:

```
tee >(grep "ERROR" > errors.txt)
```

This allows output to be processed by another command while the original stream continues.