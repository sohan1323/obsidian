
---
Displays the Linux neighbor table.

For IPv4, this is primarily the **ARP cache**.

```
ip neigh
```

Example:

```
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

Show specific interface:

```
ip neigh show dev eth0
```

Delete an entry:

```
sudo ip neigh del 192.168.1.1 dev eth0
```

### Practical use

View discovered Layer-2 neighbors:

```
ip neigh
```