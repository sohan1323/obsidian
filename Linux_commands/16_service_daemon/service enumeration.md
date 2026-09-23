
---
List running services:

```
systemctl list-units --type=service --state=running
```

List enabled services:

```
systemctl list-unit-files --type=service --state=enabled
```

Find failed services:

```
systemctl --failed
```

Inspect a service:

```
systemctl status ssh
```

Find its executable:

```
systemctl show ssh -p ExecStart
```

Find which user it runs as:

```
systemctl show ssh -p User
```

Find listening ports:

```
sudo ss -lntup
```

These commands are useful during authorized Linux system enumeration.