
---
Displays or manages Linux audit rules.

List current rules:

```
sudo auditctl -l
```

Show audit status:

```
sudo auditctl -s
```

### Important

Persistent audit rules are normally configured through audit configuration files rather than relying solely on temporary `auditctl` changes.