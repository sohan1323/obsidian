
---
Unloads a previously loaded hive.

```
reg unload HKLM\TempHive
```

Typical workflow:

```
reg load HKLM\TempHive C:\Lab\CustomHive.hiv
reg query HKLM\TempHive
reg unload HKLM\TempHive
```