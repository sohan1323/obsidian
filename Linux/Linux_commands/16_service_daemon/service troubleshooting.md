
---
Suppose:

```
sudo systemctl start nginx
```

fails.

### 1. Check status

```
systemctl status nginx
```

### 2. Check service logs

```
journalctl -u nginx
```

### 3. Check recent errors

```
journalctl -u nginx -p err -n 50
```

### 4. Check configuration

For nginx:

```
sudo nginx -t
```

### 5. Check whether the required port is already occupied

```
sudo ss -lntup | grep ':80'
```

### 6. Check service definition

```
systemctl cat nginx
```

### 7. Check process information

```
systemctl show nginx -p MainPID
```