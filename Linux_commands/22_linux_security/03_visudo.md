
---
Safely edit sudo configuration:

```
sudo visudo
```

List additional sudo configuration:

```
ls -la /etc/sudoers.d/
```

Inspect:

```
sudo ls -la /etc/sudoers.d/
```

Sudo configuration can grant permissions such as:

```
user → specific command
group → specific command
user → all commands
```