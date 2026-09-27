
---
Displays the contents of a gzip-compressed file without manually extracting it.

### Syntax

```
zcat FILE.gz
```

### Examples

```
zcat access.log.gz
```

Search compressed logs:

```
zcat access.log.gz | grep "404"
```

Multiple compressed logs:

```
zcat *.log.gz
```

### Practical security use

Search archived logs directly:

```
zcat auth.log.gz | grep "Failed password"
```