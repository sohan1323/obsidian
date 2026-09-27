
---
Captures and analyzes network packets.

This is one of the most important Linux networking troubleshooting tools.

### Syntax

```
sudo tcpdump [OPTIONS] [FILTER]
```

### Capture packets

```
sudo tcpdump
```

Specify interface:

```
sudo tcpdump -i eth0
```

List interfaces:

```
sudo tcpdump -D
```

### Don't resolve hostnames

```
sudo tcpdump -n
```

### Don't resolve ports/services

```
sudo tcpdump -nn
```

### Capture a limited number

```
sudo tcpdump -c 20
```

### Capture only TCP

```
sudo tcpdump tcp
```

### Capture only ICMP

```
sudo tcpdump icmp
```

### Capture DNS

```
sudo tcpdump -i eth0 port 53
```

### Capture HTTP

```
sudo tcpdump -i eth0 port 80
```

### Capture traffic from an IP

```
sudo tcpdump host 192.168.1.10
```

### Source IP

```
sudo tcpdump src host 192.168.1.10
```

### Destination IP

```
sudo tcpdump dst host 192.168.1.10
```

### Save capture

```
sudo tcpdump -i eth0 -w capture.pcap
```

Read capture:

```
tcpdump -r capture.pcap
```

### Practical security use

Capture DNS traffic:

```
sudo tcpdump -i eth0 -nn port 53
```

Capture traffic involving a host:

```
sudo tcpdump -i eth0 -nn host 10.10.10.5
```