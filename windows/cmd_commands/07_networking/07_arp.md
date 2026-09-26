
---
Displays and manages the ARP cache.

### Syntax

```
arp -a
arp -d address
arp -s address mac-address
```

---

## Display ARP cache

```
arp -a
```

Example:

```
Interface: 192.168.1.20
Internet Address      Physical Address      Type
192.168.1.1           aa-bb-cc-dd-ee-ff     dynamic
```

This maps:

```
IP address
    ↓
MAC address
```

---

## Delete ARP entry

```
arp -d 192.168.1.1
```

Requires appropriate permissions depending on the operation/environment.

---

## Delete all ARP entries

```
arp -d *
```

---

## Static ARP entry

```
arp -s 192.168.1.100 aa-bb-cc-dd-ee-ff
```

This manually associates an IP with a MAC address.