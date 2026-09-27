
---
### Purpose

Displays or formats the current date and time.

### Syntax

```
date [OPTION] [+FORMAT]
```

### Examples

```
date
```

```
date '+%Y-%m-%d'
```

Output:

```
2026-09-22
```

```
date '+%H:%M:%S'
```

```
20:35:42
```

Common format characters:

|Format|Meaning|
|---|---|
|`%Y`|Year|
|`%m`|Month|
|`%d`|Day|
|`%H`|Hour|
|`%M`|Minute|
|`%S`|Second|
|`%F`|`YYYY-MM-DD`|
|`%T`|`HH:MM:SS`|

### Practical use

Timestamp command output:

```
echo "$(date) - Scan completed"
```