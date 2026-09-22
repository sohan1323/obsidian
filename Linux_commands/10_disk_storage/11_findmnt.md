
---
Displays mounted filesystems in a structured way.

### Syntax

```
findmnt [OPTION] [TARGET]
```

### Examples

```
findmnt
```

Find the filesystem containing `/var`:

```
findmnt /var
```

Show filesystem type:

```
findmnt -t ext4
```

Show mount information:

```
findmnt -o SOURCE,TARGET,FSTYPE,OPTIONS
```

### Practical use

Very useful for quickly determining:

```
What device is mounted here?
What filesystem is it?
What mount options are being used?
```