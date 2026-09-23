
---
Example:

```
sudo dmesg -T | grep -i error
```

Warnings:

```
sudo dmesg -T | grep -i warning
```

Boot-related:

```
sudo dmesg -T | less
```

Hardware troubleshooting workflow:

```
Hardware problem
      ↓
dmesg
      ↓
identify device
      ↓
lspci / lsusb
      ↓
identify driver
      ↓
lspci -k
```