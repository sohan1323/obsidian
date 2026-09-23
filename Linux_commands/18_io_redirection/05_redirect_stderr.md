
---
Redirect only errors.

```
ls /etc /does-not-exist 2> errors.txt
```

Normal output appears on the terminal.

Errors go into:

```
errors.txt
```



```
command 2>> errors.log
```

Errors are appended instead of overwriting.