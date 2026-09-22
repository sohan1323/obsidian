
---
Lists PCI devices attached to the system.

Examples include:

- GPU
- network cards
- audio devices
- storage controllers
- USB controllers

### Syntax

```
lspci [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-v`|Verbose|
|`-vv`|More verbose|
|`-k`|Show kernel driver|
|`-nn`|Show PCI vendor/device IDs|
|`-s SLOT`|Show specific PCI device|

### Examples

```
lspci
```

Find GPU:

```
lspci | grep -i vga
```

Find network hardware:

```
lspci | grep -i ethernet
```

Show driver:

```
lspci -k
```

Show hardware IDs:

```
lspci -nn
```

### Practical use

Hardware enumeration:

```
lspci -nn
```

Driver investigation:

```
lspci -k
```