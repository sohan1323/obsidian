
---
Displays messages from the **kernel ring buffer**.

It is particularly useful for:

- boot messages
- hardware detection
- drivers
- USB events
- kernel errors
- filesystem events

### Syntax

```
dmesg [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-T`|Human-readable timestamps|
|`-w`|Follow new messages|
|`-H`|Human-readable output|
|`-l LEVEL`|Filter by log level|
|`-k`|Kernel messages|

### Examples

```
dmesg
```

Human-readable timestamps:

```
dmesg -T
```

Monitor new kernel messages:

```
sudo dmesg -w
```

Show errors:

```
sudo dmesg -l err
```

Find USB events:

```
dmesg | grep -i usb
```

Find network-related messages:

```
dmesg | grep -Ei 'eth|wifi|network'
```

### Practical use

When plugging in a USB device:

```
sudo dmesg -w
```

Then connect the device and observe kernel messages.