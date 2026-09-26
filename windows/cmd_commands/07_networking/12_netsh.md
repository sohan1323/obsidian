
---
`netsh` is a large command-line framework for configuring and troubleshooting Windows networking.

Think of it as:

```
netsh
 ├── interface
 ├── wlan
 ├── advfirewall
 ├── ip
 ├── winsock
 ├── winhttp
 └── ...
```

Run:

```
netsh
```

to enter interactive mode.

Or execute commands directly:

```
netsh interface show interface
```

---

## Show interfaces

```
netsh interface show interface
```

Shows network adapters and their status.

---

## Show IPv4 configuration

```
netsh interface ipv4 show config
```

---

## Show IPv6 configuration

```
netsh interface ipv6 show config
```

---

## Show TCP configuration

```
netsh interface tcp show global
```

---

## Reset TCP/IP

```
netsh int ip reset
```

This is a troubleshooting operation and may require a restart.

---

## Reset Winsock

```
netsh winsock reset
```

Often used when Windows networking components are malfunctioning.

---

# `netsh advfirewall`

Windows Firewall management.

### Show firewall state

```
netsh advfirewall show allprofiles
```

### Show firewall rules

```
netsh advfirewall firewall show rule name=all
```

### Show a specific rule

```
netsh advfirewall firewall show rule name="File and Printer Sharing (Echo Request - ICMPv4-In)"
```

### Enable firewall

```
netsh advfirewall set allprofiles state on
```

### Disable firewall

```
netsh advfirewall set allprofiles state off
```

Avoid disabling the firewall on production systems unless you have an authorized troubleshooting reason and a controlled maintenance window.

---

# `netsh wlan`

For Wi-Fi configuration.

### Show Wi-Fi interfaces

```
netsh wlan show interfaces
```

### Show saved WLAN profiles

```
netsh wlan show profiles
```

### Show a specific profile

```
netsh wlan show profile name="WiFiName"
```

This is useful for troubleshooting wireless configuration.