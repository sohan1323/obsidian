
---
`wmic` was historically used for WMI-based system information.

For example, older systems/scripts may contain:

```
wmic diskdrive get model,size
```

or:

```
wmic logicaldisk get name,size,freespace
```

However, **WMIC is deprecated/removed on some newer Windows configurations**.

Modern PowerShell/WMI/CIM commands are preferred.

You should recognize `wmic` when encountering older Windows administration scripts and security tooling.