
---
Command-line interface for **NetworkManager**.

### Syntax

```
nmcli [OPTIONS] OBJECT COMMAND
```

Common objects:

```
device
connection
general
radio
```

### Examples

Show network devices:

```
nmcli device
```

Show connections:

```
nmcli connection show
```

Show active connections:

```
nmcli connection show --active
```

Show detailed device information:

```
nmcli device show
```

Show Wi-Fi networks:

```
nmcli device wifi list
```

Turn Wi-Fi off:

```
nmcli radio wifi off
```

Turn Wi-Fi on:

```
nmcli radio wifi on
```

### Practical use

NetworkManager-based systems:

```
nmcli device status
```