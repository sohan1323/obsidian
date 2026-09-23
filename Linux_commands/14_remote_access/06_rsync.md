
---
Efficiently synchronizes files and directories.

It is particularly useful for:

- backups
- large directory transfers
- incremental synchronization
- remote administration

### Syntax

```
rsync [OPTIONS] SOURCE DESTINATION
```

### Local synchronization

```
rsync -av source/ destination/
```

### Important options

|Option|Purpose|
|---|---|
|`-a`|Archive mode|
|`-v`|Verbose|
|`-h`|Human-readable|
|`-r`|Recursive|
|`-n`|Dry run|
|`-P`|Progress + partial transfers|
|`--delete`|Delete destination files not in source|
|`-e`|Specify remote shell|
|`-z`|Compress during transfer|

### Remote upload

```
rsync -av project/ user@192.168.1.10:/tmp/project/
```

Remote download:

```
rsync -av user@192.168.1.10:/tmp/project/ ./project/
```

### Dry run

Before making changes:

```
rsync -av --dry-run source/ destination/
```

or:

```
rsync -avn source/ destination/
```

### Progress

```
rsync -avP largefile.iso user@192.168.1.10:/tmp/
```

### Delete destination differences

```
rsync -av --delete source/ destination/
```

Be careful with `--delete`.