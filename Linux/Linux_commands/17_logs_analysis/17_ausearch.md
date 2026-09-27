
---
Searches Linux **auditd** audit logs.

Available when the audit subsystem/tools are installed.

### Search authentication events

```
sudo ausearch -m USER_LOGIN
```

### Search by user ID

```
sudo ausearch -ui 1000
```

### Search by executable

```
sudo ausearch -x /usr/bin/sudo
```

### Search by date

```
sudo ausearch -ts today
```

### Practical security use

Audit logs can provide more structured security events than ordinary application logs.