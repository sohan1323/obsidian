
---
### Foreground

A command running in the foreground occupies your terminal:

```
ping 127.0.0.1
```

The shell waits for it.

You normally cannot enter another command until it finishes or you interrupt it.

### Background

A command can run in the background:

```
ping 127.0.0.1 &
```

The shell immediately gives you the prompt back.

```
Terminal
   │
   ├── foreground → command controls terminal
   │
   └── background → shell remains usable
```