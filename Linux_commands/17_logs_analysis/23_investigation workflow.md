
---
When investigating a suspicious event:

### 1. Check current users

```
who
```

### 2. Check recent logins

```
last -n 30
```

### 3. Check failed logins

```
sudo lastb -n 30
```

### 4. Check SSH logs

```
sudo journalctl -u ssh
```

or:

```
sudo grep "sshd" /var/log/auth.log
```

### 5. Check errors

```
sudo journalctl -p err
```

### 6. Check kernel events

```
sudo journalctl -k
```

### 7. Check audit logs if enabled

```
sudo ausearch -ts today
```

### 8. Check scheduled activity

```
systemctl list-timers --all
```

### 9. Check running processes

```
ps aux
```