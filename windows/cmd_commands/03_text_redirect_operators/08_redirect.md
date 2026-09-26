
---
The `>` operator redirects **standard output** to a file.

### Example

```
dir > files.txt
```

Instead of displaying the directory listing on the screen, CMD writes it to:

```
files.txt
```

### Important

`>` **overwrites** the destination.

```
echo First > test.txt
echo Second > test.txt
```

The file contains only:

```
Second
```