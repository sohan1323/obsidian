
---
Keeps private keys available in memory so you don't repeatedly enter their passphrases.

Start an agent:

```
eval "$(ssh-agent -s)"
```

Add a key:

```
ssh-add ~/.ssh/id_ed25519
```

List loaded keys:

```
ssh-add -l
```

Remove a key:

```
ssh-add -d ~/.ssh/id_ed25519
```

Remove all:

```
ssh-add -D
```

### Practical use

Useful when working with multiple SSH connections requiring the same key.