
---
When investigating an installed program, useful commands include:

### Which executable?

```
which nmap
```

### What package owns it?

```
dpkg -S "$(which nmap)"
```

### Package details

```
dpkg -s nmap
```

### Files installed

```
dpkg -L nmap
```

### Package version

```
apt-cache policy nmap
```

This gives a useful package investigation chain:

```
Program
   ↓
which
   ↓
Executable path
   ↓
dpkg -S
   ↓
Package
   ↓
dpkg -s / apt-cache policy
   ↓
Version/details
```