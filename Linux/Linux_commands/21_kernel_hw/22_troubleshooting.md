
---
For a device that isn't working:

```
Device problem
      ↓
dmesg
      ↓
lspci / lsusb
      ↓
identify device
      ↓
lspci -k
      ↓
identify driver
      ↓
lsmod
      ↓
modinfo driver
```

Example for a PCI device:

```
lspci -k
```

Look for:

```
Kernel driver in use:
Kernel modules:
```



# Security-Relevant Kernel Enumeration

For authorized security assessment:

```
uname -a
```

Kernel version:

```
uname -r
```

Architecture:

```
uname -m
```

CPU:

```
lscpu
```

Kernel parameters:

```
sysctl -a
```

Loaded modules:

```
lsmod
```

Kernel command line:

```
cat /proc/cmdline
```

Kernel messages:

```
sudo dmesg -T
```

ASLR:

```
sysctl kernel.randomize_va_space
```

This information helps establish:

```
OS/kernel version
        ↓
architecture
        ↓
hardware
        ↓
loaded modules
        ↓
kernel configuration
        ↓
security mitigations
```

