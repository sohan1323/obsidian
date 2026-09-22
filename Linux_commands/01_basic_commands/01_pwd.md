
---
**Purpose:** Shows the **current working directory**.

### Syntax

```bash
pwd [OPTION]
```

### Arguments / options

|Option|Meaning|
|---|---|
|`-L`|Show logical path, following symbolic links|
|`-P`|Show physical path, resolving symbolic links|

### Examples

```bash
pwd
```

Output:

```bash
/home/user
```

Show physical path:

```bash
pwd -P
```

Show logical path:

```bash
pwd -L
```
