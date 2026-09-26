
---
`<` redirects a file into a command's standard input.

For example:

```
sort < names.txt
```

Instead of `sort` reading from the console, it receives input from `names.txt`.

Conceptually:

```
names.txt
    ↓
   sort
    ↓
  output
```