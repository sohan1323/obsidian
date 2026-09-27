
---
Lists PCI devices.

```
lspci
```

Typical devices:

```
Ethernet controller
Network controller
VGA controller
Audio device
USB controller
```

For more detail:

```
lspci -v
```

Very detailed:

```
lspci -vv
```

Show numeric vendor/device IDs:

```
lspci -nn
```

Show the kernel driver:

```
lspci -k
```

This is particularly useful for GPU and network-driver troubleshooting.