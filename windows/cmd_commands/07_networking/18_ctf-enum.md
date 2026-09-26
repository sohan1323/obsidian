
---
On a Windows machine you are authorized to assess:

```
hostname
whoami /all
ipconfig /all
route print
arp -a
netstat -ano
tasklist /svc
net share
net use
```

Then filter useful information:

```
ipconfig /all | findstr /i "IPv4 IPv6 DNS Gateway DHCP"
```

```
netstat -ano | findstr "LISTENING"
```

```
tasklist | findstr /i "powershell cmd ssh"
```

```
arp -a
```

This gives you a basic picture of:

```
Host
 │
 ├── Identity
 ├── IP configuration
 ├── Routes
 ├── Neighbor cache
 ├── Listening ports
 ├── Processes
 └── Network shares
```