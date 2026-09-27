
---
Extracts ZIP archives.

### Syntax

```
unzip [OPTIONS] ARCHIVE
```

### Important options

|Option|Purpose|
|---|---|
|`-l`|List contents|
|`-t`|Test archive|
|`-d DIR`|Extract to directory|
|`-q`|Quiet|
|`-o`|Overwrite without prompting|
|`-n`|Never overwrite|

### Examples

Extract:

```
unzip backup.zip
```

Extract elsewhere:

```
unzip backup.zip -d /tmp/backup
```

List contents:

```
unzip -l backup.zip
```

Test archive:

```
unzip -t backup.zip
```

### Practical security use

Before extracting an unknown ZIP:

```
unzip -l suspicious.zip
```

Then test it:

```
unzip -t suspicious.zip
```