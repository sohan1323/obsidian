
---
`format` is the standalone CMD formatting command.

### Syntax

```
format <drive>: /fs:<filesystem>
```

Example:

```
format D: /fs:NTFS
```

Quick format:

```
format D: /fs:NTFS /q
```

Set volume label:

```
format D: /fs:NTFS /v:LAB
```

Important switches:

|Switch|Purpose|
|---|---|
|`/FS:`|Filesystem|
|`/Q`|Quick format|
|`/V:`|Volume label|
|`/X`|Force dismount|
|`/P:`|Overwrite sectors|

**Never experiment with `format` on your Windows system volume unless you intentionally want to destroy/reinstall it.**