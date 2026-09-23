
---
Adds or removes APT repositories or PPAs where supported.

### Add repository

```
sudo add-apt-repository ppa:example/repository
```

Then:

```
sudo apt update
```

### Remove repository

```
sudo add-apt-repository --remove ppa:example/repository
```

### Important

Only add repositories you trust.

A repository can provide packages that execute with high privileges during installation.