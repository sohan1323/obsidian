
---
Linux exposes standard streams through special files:

```
/dev/stdin
/dev/stdout
/dev/stderr
```

Example:

```
echo "Hello" > /dev/stdout
```

You can also refer to the file descriptors:

```
/dev/fd/0
/dev/fd/1
/dev/fd/2
```

---

# File Descriptors

Every open file/stream has a file descriptor.

The standard ones:

|FD|Name|Purpose|
|---|---|---|
|`0`|stdin|Input|
|`1`|stdout|Normal output|
|`2`|stderr|Error output|

Example:

```
echo "hello" >&1
```

Explicitly sends output to stdout.

```
echo "error" >&2
```

Sends output to stderr.

This is useful in scripts:

```
echo "ERROR: file not found" >&2
```