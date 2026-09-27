
---
Copies your public SSH key to a remote user's `authorized_keys`.

### Syntax

```
ssh-copy-id [OPTIONS] USER@HOST
```

### Example

```
ssh-copy-id user@192.168.1.10
```

Specify a key:

```
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@192.168.1.10
```

Afterward:

```
ssh user@192.168.1.10
```

can authenticate using the configured key.