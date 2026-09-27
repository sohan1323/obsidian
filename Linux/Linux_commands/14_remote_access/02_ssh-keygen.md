
---
Creates and manages SSH keys.

Typical key pair:

```
Private key → ~/.ssh/id_ed25519
Public key  → ~/.ssh/id_ed25519.pub
```

### Syntax

```
ssh-keygen [OPTIONS]
```

### Generate Ed25519 key

```
ssh-keygen -t ed25519
```

Specify output file:

```
ssh-keygen -t ed25519 -f ~/.ssh/lab_key
```

Specify RSA:

```
ssh-keygen -t rsa -b 4096
```

### Important options

|Option|Purpose|
|---|---|
|`-t TYPE`|Key type|
|`-b BITS`|Key size|
|`-f FILE`|Output filename|
|`-C COMMENT`|Key comment|
|`-N PASSPHRASE`|Set passphrase|
|`-y`|Derive public key from private key|
|`-l`|Show fingerprint|

### View fingerprint

```
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

### Extract public key from private key

```
ssh-keygen -y -f ~/.ssh/id_ed25519
```