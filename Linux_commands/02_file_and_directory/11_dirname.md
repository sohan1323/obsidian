
---
**Purpose:** Extract the directory portion of a path.

### Syntax

```
dirname PATH
```

### Example

```
dirname /home/user/documents/file.txt
```

Output:

```
/home/user/documents
```

### Practical use

Useful in shell scripts when you need to determine the directory containing a file.

Example:

```
script="/opt/tools/test.sh"
dirname "$script"
```

Output:

```
/opt/tools
```