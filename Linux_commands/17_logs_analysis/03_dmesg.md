
---
Displays kernel messages.

```
dmesg
```

Human-readable timestamps:

```
dmesg -T
```

Follow new kernel messages:

```
sudo dmesg -w
```

Errors:

```
sudo dmesg -l err
```

Warnings:

```
sudo dmesg -l warn
```

Search:

```
dmesg | grep -i usb
```

Network:

```
dmesg | grep -Ei 'network|eth|wifi'
```

### Practical use

Investigate:

- hardware detection
- driver errors
- USB devices
- kernel errors
- filesystem events