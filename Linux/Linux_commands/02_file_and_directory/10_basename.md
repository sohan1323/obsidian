
---
**Purpose:** Extract the filename from a path.

### Syntax

```
basename PATH [SUFFIX]
```

### Example

```
basename /home/user/documents/file.txt
```

Output:

```
file.txt
```

Remove suffix:

```
basename /home/user/file.txt .txt
```

Output:

```
file
```

### Practical use

Very common in shell scripts.

```
file="/var/log/auth.log"
basename "$file"
```

Output:

```
auth.log
```