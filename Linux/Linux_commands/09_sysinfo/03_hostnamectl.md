
---
### Purpose

Displays or manages the system hostname and related system information.

It is commonly available on systems using **systemd**.

### Syntax

```
hostnamectl [OPTIONS] [COMMAND]
```

### Examples

```
hostnamectl
```

Typical information:

```
Static hostname: kali
Operating System: Kali GNU/Linux
Kernel: Linux 6.x
Architecture: x86-64
```

Set hostname:

```
sudo hostnamectl set-hostname lab-server
```

Display only hostname:

```
hostnamectl hostname
```

### Practical use

Quickly identify:

- hostname
- OS
- kernel
- architecture
- virtualization information