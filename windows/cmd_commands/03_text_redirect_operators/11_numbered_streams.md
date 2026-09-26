
---
Windows CMD uses numbered streams.

The important ones are:

```
0 = stdin
1 = stdout
2 = stderr
```

Therefore:

```
2>
```

redirects **error output**.

### Example

```
dir C:\DoesNotExist 2> errors.txt
```

The error goes into:

```
errors.txt
```

while normal output still goes to the console.

# `2>&1`

This combines standard error with standard output.

```
command > output.txt 2>&1
```

Meaning:

```
stdout ──┐
         ├──> output.txt
stderr ──┘
```

Example:

```
dir C:\Windows C:\DoesNotExist > result.txt 2>&1
```

Both successful output and error messages are written to `result.txt`.

### Important ordering

This:

```
command > output.txt 2>&1
```

is correct when you want both streams in the file.