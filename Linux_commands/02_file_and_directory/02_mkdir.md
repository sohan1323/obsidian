
---
**Purpose:** Create directories.

### Syntax

```
mkdir [OPTION]... DIRECTORY...
```

### Important options

|Option|Meaning|
|---|---|
|`-p`|Create parent directories if needed|
|`-m MODE`|Set permissions|
|`-v`|Display what is being created|

### Examples

Create directory:

```
mkdir projects
```

Create multiple directories:

```
mkdir logs backups scripts
```

Create nested directories:

```
mkdir -p project/src/python
```

Without `-p`, this can fail if `project/src` doesn't exist.

Verbose:

```
mkdir -v test
```

Create directory with specific permissions:

```
mkdir -m 700 private
```

The directory will initially have permissions equivalent to:

```
drwx------
```