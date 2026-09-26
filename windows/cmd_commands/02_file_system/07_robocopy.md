
---
`robocopy` = **Robust File Copy**.

For serious Windows administration, this is much more important than `xcopy`.

It supports:

- recursive copying
- retries
- network shares
- mirroring
- file attributes
- timestamps
- ACLs
- logging
- restartable transfers

### Basic syntax

```
robocopy source destination [files] [options]
```

### Basic example

```
robocopy C:\Projects D:\Backup
```

### Recursive

```
robocopy C:\Projects D:\Backup /E
```

`/E` copies subdirectories including empty directories.

---

## Important `robocopy` switches

### `/S`

Copy subdirectories, excluding empty ones.

```
robocopy C:\Data D:\Backup /S
```

### `/E`

Copy subdirectories including empty ones.

```
robocopy C:\Data D:\Backup /E
```

### `/MIR`

Mirror source to destination.

```
robocopy C:\Data D:\Backup /MIR
```

**Be careful:** `/MIR` can delete files from the destination if they no longer exist in the source.

### `/Z`

Restartable mode.

```
robocopy C:\Data \\Server\Backup /E /Z
```

### `/ZB`

Uses restartable mode and falls back to backup mode when access is denied.

```
robocopy C:\Data D:\Backup /E /ZB
```

### `/R`

Number of retries.

```
robocopy C:\Data D:\Backup /R:3
```

### `/W`

Wait time between retries.

```
robocopy C:\Data D:\Backup /R:3 /W:5
```

### `/XO`

Exclude older files.

```
robocopy C:\Data D:\Backup /XO
```

### `/MAXAGE`

Only copy files newer than a specified age.

```
robocopy C:\Data D:\Backup /MAXAGE:30
```

### `/MINAGE`

Only copy files older than a specified age.

```
robocopy C:\Data D:\Backup /MINAGE:30
```

### `/MAX`

Maximum file size.

```
robocopy C:\Data D:\Backup /MAX:10000000
```

### `/LOG`

Write output to a log file.

```
robocopy C:\Data D:\Backup /E /LOG:backup.log
```

### `/TEE`

Display output and write it to the log.

```
robocopy C:\Data D:\Backup /E /LOG:backup.log /TEE
```

### `/COPY`

Controls what gets copied.

```
robocopy C:\Data D:\Backup /COPY:DAT
```

Common flags:

|Flag|Meaning|
|---|---|
|`D`|Data|
|`A`|Attributes|
|`T`|Timestamps|
|`S`|NTFS ACL/security|
|`O`|Owner|
|`U`|Auditing information|

For example:

```
robocopy C:\Data D:\Backup /COPY:DATS
```

copies:

```
Data
Attributes
Timestamps
Security ACLs
```