
---
Creates ZIP archives.

ZIP is particularly common when exchanging files between Linux and Windows.

### Syntax

```
zip [OPTIONS] ARCHIVE FILES...
```

### Important options

|Option|Purpose|
|---|---|
|`-r`|Recursively include directories|
|`-9`|Maximum compression|
|`-q`|Quiet|
|`-e`|Encrypt archive|
|`-u`|Update archive|
|`-d`|Delete from archive|

### Examples

Create ZIP:

```
zip backup.zip file1.txt file2.txt
```

Directory:

```
zip -r project.zip project/
```

Maximum compression:

```
zip -9 -r project.zip project/
```

Add/update files:

```
zip -u backup.zip newfile.txt
```

Delete a file from archive:

```
zip -d backup.zip file.txt
```