
---
Loads a registry hive into another registry key.

### Syntax

```
reg load KeyName FileName
```

Example:

```
reg load HKLM\TempHive C:\Lab\CustomHive.hiv
```

You can then query it:

```
reg query HKLM\TempHive
```