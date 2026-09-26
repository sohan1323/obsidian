
---
Services are registered in the Registry.

A major location is:

```
HKLM\SYSTEM\CurrentControlSet\Services
```

Query:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Services"
```

Specific service:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Services\Spooler"
```

You can also inspect:

```
reg query "HKLM\SYSTEM\CurrentControlSet\Services\Spooler" /v ImagePath
```

This can show the service executable configuration.

Compare it with:

```
sc qc Spooler
```