
---
Shows network interface statistics.

```
ip -s link
```

Look for:

- RX packets
- TX packets
- dropped packets
- errors

Specific interface:

```
ip -s link show eth0
```

### Practical use

Investigate packet errors or drops.