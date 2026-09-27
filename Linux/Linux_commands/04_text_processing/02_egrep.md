
---
**Purpose:** Search using **extended regular expressions**.

`egrep` historically means:

```
grep -E
```

### Syntax

```
egrep [OPTIONS] PATTERN FILE
```

Example:

```
egrep "error|warning|failed" logfile.txt
```

Equivalent modern form:

```
grep -E "error|warning|failed" logfile.txt
```

### Important

Prefer:

```
grep -E
```

instead of `egrep`.

`egrep` exists mainly for compatibility with older usage.