
---
Commonly used on shared directories such as `/tmp`.

```
ls -ld /tmp
```

Typical:

```
drwxrwxrwt
```

The `t` indicates the sticky bit.

It restricts deletion/renaming of files in the directory according to ownership/privilege rules.