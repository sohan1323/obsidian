
---
Modern Bash syntax:

```
command &> output.txt
```

Equivalent to:

```
command > output.txt 2>&1
```

Example:

```
ls /etc /does-not-exist > result.txt 2>&1
```

Both normal output and errors go into `result.txt`.



# Understanding `2>&1`

This is important.

```
command > output.txt 2>&1
```

Means:

```
stdout → output.txt
stderr → wherever stdout currently goes
```

So:

```
1 → output.txt
2 → 1
```

Both end up in the file.

### Order matters

This:

```
command > output.txt 2>&1
```

is different from:

```
command 2>&1 > output.txt
```

The first sends both streams to the file.

The second sends stderr to the terminal while stdout goes to the file.