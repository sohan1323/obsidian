
---
### Check interface

```
ip link
```

### Check IP

```
ip addr
```

### Check route

```
ip route
```

### Check gateway

```
ip route | grep default
```

### Test gateway

```
ping -c 4 192.168.1.1
```

### Test Internet by IP

```
ping -c 4 8.8.8.8
```

### Test DNS

```
dig example.com
```

### Test HTTP

```
curl -I https://example.com
```

### Inspect packets

```
sudo tcpdump -i eth0 -nn
```