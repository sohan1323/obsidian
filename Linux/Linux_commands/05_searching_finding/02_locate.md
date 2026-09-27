
---
**Purpose:** Quickly search for files using a prebuilt database.

### Syntax

```
locate [OPTIONS] PATTERN
```

### Examples

```
locate passwd
```

Find files containing `passwd` in their path.

```
locate ssh_config
```

Case-insensitive:

```
locate -i README
```

Limit results:

```
locate -n 10 passwd
```

### Important difference

`find`:

```
Searches the filesystem directly
```

`locate`:

```
Searches a database
```

Therefore `locate` is usually much faster, but its database can be outdated.