
---
Parentheses execute commands in a subshell.

```
(
    cd /tmp
    echo "$PWD"
)
```

The directory change doesn't affect the parent shell.

Compare:

```
cd /tmp
```

which changes the current shell's directory.