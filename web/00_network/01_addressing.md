
---
An **IP address (Internet Protocol address)** is a logical address assigned to a network interface so that devices can be **identified and reached on an IP network**.

# Two Main Versions of IP

There are two major versions:

|Version|Example|Address Size|
|---|---|---|
|**IPv4**|`192.168.1.10`|32 bits|
|**IPv6**|`2001:db8::1`|128 bits|
An IPv4 address generally contains two logical parts:

```
IP Address
┌───────────────┬───────────────┐
│ Network part  │   Host part   │
└───────────────┴───────────────┘
```

For example:

```
192.168.1.10/24
```

With `/24`:

```
Network: 192.168.1.0
Host:    10
```


# Public vs Private IP

This is extremely important.

## Private IP

Private IP addresses are intended for use **inside private networks**.

They are **not directly routable across the public Internet**.

The three IPv4 private ranges are:

|Private Range|CIDR|
|---|---|
|`10.0.0.0 – 10.255.255.255`|`10.0.0.0/8`|
|`172.16.0.0 – 172.31.255.255`|`172.16.0.0/12`|
|`192.168.0.0 – 192.168.255.255`|`192.168.0.0/16`|

Examples:

```
10.0.0.5
10.20.30.40

172.16.1.10
172.20.5.15

192.168.1.10
192.168.100.20
```

These are commonly found in:

- Home networks
- Office networks
- VMware labs
- Docker networks
- Internal enterprise networks
- Cloud private networks

---

# 6. Public IP

A **public IP address** is an address that can be routed across the public Internet.

For example, your home router might have:

```
Private network
     │
     ↓
192.168.1.10
     │
     ↓
Router
     │
     ↓
Public IP
     │
     ↓
Internet
```

Your laptop may have:

```
192.168.1.10
```

while your router has a public IP assigned by your ISP.

This commonly involves **NAT (Network Address Translation)**.


| Feature                      | Private IP     | Public IP                    |
| ---------------------------- | -------------- | ---------------------------- |
| Used inside private networks | ✅              | Possible, but unnecessary    |
| Routable on Internet         | ❌              | ✅                            |
| Globally unique              | No             | Yes, generally               |
| Common example               | `192.168.1.10` | ISP-assigned address         |
| Common location              | LAN            | Internet                     |
| NAT commonly involved        | Yes            | Often the public side of NAT |

| Range / Address   | Purpose                                            |
| ----------------- | -------------------------------------------------- |
| `10.0.0.0/8`      | Private                                            |
| `172.16.0.0/12`   | Private                                            |
| `192.168.0.0/16`  | Private                                            |
| `127.0.0.0/8`     | Loopback                                           |
| `169.254.0.0/16`  | Link-local / APIPA                                 |
| `0.0.0.0`         | Unspecified / special meaning depending on context |
| `255.255.255.255` | Limited broadcast                                  |
| `224.0.0.0/4`     | Multicast                                          |
| `100.64.0.0/10`   | Carrier-grade NAT                                  |
# Static vs Dynamic IP

Another classification is based on **how the address is assigned**.

### Static IP

An IP address is manually/configurationally assigned and intended to remain stable.

Example:

```
Server → 192.168.1.50
```

Useful for:

- Servers
- Network infrastructure
- Security appliances
- Some printers

### Dynamic IP

An IP address is automatically assigned, commonly using **DHCP**.

Example:

```
Laptop
   ↓
DHCP Server
   ↓
192.168.1.25
```

The address can change later.



# Unicast, Broadcast, Multicast, Anycast

These describe **how traffic is delivered**, rather than whether an address is public/private.

### Unicast

One sender → one receiver.

```
A ─────────→ B
```

Example:

```
Your computer → Web server
```

---

### Broadcast

One sender → all applicable devices on the local broadcast domain.

```
        ┌→ A
Sender ─┼→ B
        ├→ C
        └→ D
```

IPv4 broadcast example:

```
255.255.255.255
```

---

### Multicast

One sender → multiple subscribed receivers.

```
       ┌→ A
       ├→ B
Sender ┼→ C
       └→ D
```

IPv4 multicast:

```
224.0.0.0 – 239.255.255.255
```

---

### Anycast

One address is associated with multiple possible nodes, and routing typically delivers traffic to the **nearest/best available node** according to the routing system.

Common in large distributed services.


# MAC Address

A **MAC (Media Access Control) address** is a **link-layer address** associated with a network interface.

It is used for communication on the **local network/link**.

Example:

```
00:1A:2B:3C:4D:5E
```

Another representation:

```
00-1A-2B-3C-4D-5E
```

A typical MAC address is **48 bits (6 bytes)**.

```
00 : 1A : 2B : 3C : 4D : 5E
│───────────────│ │───────────│
   OUI/vendor       Interface
    portion           portion
```

The exact interpretation can vary with address type, and not every MAC is globally assigned to a hardware manufacturer.