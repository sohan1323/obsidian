
---
Securely copies files between systems using SSH.

### Syntax

```
scp [OPTIONS] SOURCE DESTINATION
```

---

### Local → remote

```
scp file.txt user@192.168.1.10:/tmp/
```

### Remote → local

```
scp user@192.168.1.10:/tmp/file.txt .
```

### Directory → remote

```
scp -r project/ user@192.168.1.10:/tmp/
```

### Specify SSH port

```
scp -P 2222 file.txt user@192.168.1.10:/tmp/
```

### Specify private key

```
scp -i ~/.ssh/id_ed25519 file.txt user@192.168.1.10:/tmp/
```

### Important options

| Option    | Purpose                   |
| --------- | ------------------------- |
| `-r`      | Recursive                 |
| `-P PORT` | SSH port                  |
| `-i FILE` | Private key               |
| `-p`      | Preserve timestamps/modes |
| `-q`      | Quiet                     |
| `-v`      | Verbose                   |