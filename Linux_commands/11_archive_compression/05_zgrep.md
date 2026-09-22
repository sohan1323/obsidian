
---
Searches inside gzip-compressed files.

### Syntax

```
zgrep [OPTIONS] PATTERN FILE.gz
```

### Examples

```
zgrep "error" application.log.gz
```

Case-insensitive:

```
zgrep -i "failed password" auth.log.gz
```

Show line numbers:

```
zgrep -n "404" access.log.gz
```

Recursive:

```
zgrep -r "password" /var/log/
```