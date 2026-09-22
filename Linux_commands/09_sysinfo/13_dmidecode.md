
---
Reads hardware information from the system's **DMI/SMBIOS tables**.

It can reveal:

- BIOS information
- motherboard
- manufacturer
- system model
- RAM
- CPU
- serial information

### Syntax

```
sudo dmidecode [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-t TYPE`|Display specific hardware category|
|`-s STRING`|Display specific DMI string|
|`-q`|Less verbose|
|`-u`|Raw output|

### Examples

System information:

```
sudo dmidecode -t system
```

BIOS:

```
sudo dmidecode -t bios
```

Memory:

```
sudo dmidecode -t memory
```

CPU:

```
sudo dmidecode -t processor
```

Get system manufacturer:

```
sudo dmidecode -s system-manufacturer
```

### Practical use

Hardware enumeration:

```
sudo dmidecode -t system
```

Memory information:

```
sudo dmidecode -t memory
```