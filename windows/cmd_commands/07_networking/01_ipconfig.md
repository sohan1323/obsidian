
---
Displays and manages IP configuration.

### Syntax

```
ipconfig [/allcompartments] [/all] [/renew [adapter]] [/release [adapter]]
         [/renew6 [adapter]] [/release6 [adapter]]
         [/flushdns] [/displaydns] [/registerdns]
         [/showclassid adapter] [/setclassid adapter [classid]]
         [/showclassid6 adapter] [/setclassid6 adapter [classid]]
```

---

## Basic

```
ipconfig
```

Typical output:

```
Windows IP Configuration

Ethernet adapter Ethernet:

   IPv4 Address. . . . . . : 192.168.1.20
   Subnet Mask . . . . . . : 255.255.255.0
   Default Gateway . . . . : 192.168.1.1
```

Important information:

```
IPv4 address
Subnet mask
Default gateway
```

---

## `/all`

Displays complete configuration.

```
ipconfig /all
```

You'll see:

- hostname
- adapter description
- MAC address
- DHCP status
- IPv4
- IPv6
- subnet mask
- gateway
- DNS servers
- DHCP server
- lease information

This should be one of the first commands you know for Windows network troubleshooting.

---

## `/release`

Releases the current DHCP IPv4 lease.

```
ipconfig /release
```

Specific adapter:

```
ipconfig /release "Ethernet"
```

---

## `/renew`

Requests a new DHCP lease.

```
ipconfig /renew
```

Specific adapter:

```
ipconfig /renew "Ethernet"
```

Common troubleshooting sequence:

```
ipconfig /release
ipconfig /renew
```

---

## `/flushdns`

Clears the local DNS resolver cache.

```
ipconfig /flushdns
```

Example output:

```
Successfully flushed the DNS Resolver Cache.
```

Useful after DNS changes or when troubleshooting stale DNS information.

---

## `/displaydns`

Displays cached DNS entries.

```
ipconfig /displaydns
```

This can show locally cached DNS information.

---

## `/registerdns`

Attempts to refresh/register DNS information.

```
ipconfig /registerdns
```

Useful primarily in Windows domain/DNS environments.