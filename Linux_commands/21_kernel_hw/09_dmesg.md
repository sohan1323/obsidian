
---
Displays the kernel's message buffer.

```
dmesg
```

Human-readable timestamps:

```
sudo dmesg -T
```

Follow new kernel messages:

```
sudo dmesg -w
```

Show only warnings/errors:

```
sudo dmesg -l warn,err
```

Search:

```
dmesg | grep -i usb
```

GPU:

```
dmesg | grep -i gpu
```

Network:

```
dmesg | grep -Ei "eth|wlan|wifi|network"
```