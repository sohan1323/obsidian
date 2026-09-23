
---
If:

```
ssh user@192.168.1.10
```

fails:

### 1. Test connectivity

```
ping -c 4 192.168.1.10
```

### 2. Test port 22

```
nc -vz 192.168.1.10 22
```

### 3. Check local routing

```
ip route get 192.168.1.10
```

### 4. Check SSH service remotely if you have console access

```
sudo ss -lntp | grep ':22'
```

### 5. Debug SSH

```
ssh -vvv user@192.168.1.10
```

### 6. Check SSH host-key entry

```
ssh-keygen -F 192.168.1.10
```