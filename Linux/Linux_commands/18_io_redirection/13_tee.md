
---
`tee` copies stdin to both:

```
terminal
+
file
```

Example:

```
ls | tee files.txt
```

You see the output and it is also saved to:

```
files.txt
```

### Append

```
ls | tee -a files.txt
```

`-a` means append.