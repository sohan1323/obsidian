
---
**Purpose:** Display jobs managed by the current shell.

### Syntax

```
jobs [OPTIONS]
```

Example:

```
jobs
```

Possible output:

```
[1]+  Running    ./script.sh &
[2]-  Stopped    vim file.txt
```

### Important options

| Option | Meaning          |
| ------ | ---------------- |
| `-l`   | Include PIDs     |
| `-p`   | Show process IDs |
| `-r`   | Running jobs     |
| `-s`   | Stopped jobs     |