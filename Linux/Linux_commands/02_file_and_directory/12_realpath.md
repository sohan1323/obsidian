
---
**Purpose:** Convert a path into its absolute, canonical path.

### Syntax

```
realpath [OPTION] PATH
```

### Examples

```
realpath file.txt
```

Possible output:

```
/home/user/project/file.txt
```

For a symbolic link:

```
realpath symlink.txt
```

It resolves the link to its actual target.

### Useful option

|Option|Meaning|
|---|---|
|`-e`|Require all components to exist|
|`-m`|Allow missing components|
|`-s`|Don't resolve symbolic links|

### Example

```
realpath -e /etc/passwd
```