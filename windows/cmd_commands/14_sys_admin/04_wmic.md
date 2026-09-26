
---
`wmic` is a legacy WMI command-line interface and may not be available on newer Windows installations.

Examples you may encounter in older scripts:

```
wmic os get caption,version
```

CPU:

```
wmic cpu get name
```

RAM:

```
wmic computersystem get totalphysicalmemory
```

Disk:

```
wmic logicaldisk get name,size,freespace
```

Modern Windows increasingly uses PowerShell/CIM instead.