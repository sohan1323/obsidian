
---
Changes a file's size.

Create an empty 1 KB file:

```
truncate -s 1K file
```

Increase:

```
truncate -s 10K file
```

Empty a file:

```
truncate -s 0 file
```

Be careful: truncating a file destroys its existing contents beyond the new size.