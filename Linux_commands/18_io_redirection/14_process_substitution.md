
---
Bash can make command output appear like a temporary file.

Example:

```
diff <(ls dir1) <(ls dir2)
```

Conceptually:

```
ls dir1 ──┐
          ├── diff
ls dir2 ──┘
```

Another example:

```
cat <(printf "one\ntwo\n")
```

This is Bash-specific functionality.