
---
Checks filesystem integrity and, when requested, repairs filesystem errors.

### Basic

```
chkdsk C:
```

### Check and repair

```
chkdsk C: /f
```

`/f` attempts to fix filesystem errors.

### Locate bad sectors

```
chkdsk C: /r
```

`/r` attempts to locate bad sectors and recover readable information.

### Online scan

```
chkdsk C: /scan
```

Performs an online NTFS scan.

### Force dismount

```
chkdsk D: /f /x
```

`/x` forces the volume to dismount when necessary.

### Important switches

|Switch|Purpose|
|---|---|
|`/f`|Fix filesystem errors|
|`/v`|Verbose output|
|`/r`|Locate bad sectors/recover readable data|
|`/x`|Force dismount|
|`/i`|Less intensive NTFS index check|
|`/scan`|Online NTFS scan|

Example:

```
chkdsk D: /f
```
