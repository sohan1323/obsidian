
---
**Purpose:** Locates binaries, source files, and manual pages associated with a command.

### Syntax

```
whereis [OPTIONS] COMMAND
```

### Important options

|Option|Meaning|
|---|---|
|`-b`|Search only binaries|
|`-m`|Search only manual pages|
|`-s`|Search only source files|
|`-u`|Search unusual entries|

### Examples

```
whereis bash
```

Possible output:

```
bash: /usr/bin/bash /usr/share/man/man1/bash.1.gz
```

Only binary:

```
whereis -b bash
```

Only manual:

```
whereis -m bash
```