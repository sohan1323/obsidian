
---
**Purpose:** Display filesystem attributes.

### Syntax

```
lsattr [OPTIONS] [FILE]
```

Example:

```
lsattr file.txt
```

Possible output:

```
---------------------- file.txt
```

Some important attributes include:

| Attribute | Meaning                  |
| --------- | ------------------------ |
| `i`       | Immutable                |
| `a`       | Append-only              |
| `A`       | Don't update access time |
| `d`       | No dump                  |
| `S`       | Synchronous updates      |