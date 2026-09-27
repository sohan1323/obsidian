
---
Lists USB devices connected to the system.

### Syntax

```
lsusb [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-v`|Verbose information|
|`-t`|USB device tree|
|`-d`|Filter by vendor/device ID|
|`-s`|Filter by bus/device|

### Examples

```
lsusb
```

Example:

```
Bus 001 Device 002: ID 8087:0026 Intel Corp.
```

Show USB tree:

```
lsusb -t
```

Verbose information:

```
sudo lsusb -v
```

### Practical use

Identify connected USB hardware:

```
lsusb
```

USB device tree:

```
lsusb -t
```