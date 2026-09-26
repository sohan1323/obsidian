
---
Modern Windows commonly includes OpenSSH client functionality.

### Basic

```
ssh user@server
```

Example:

```
ssh student@192.168.56.10
```

### Specify port

```
ssh -p 2222 student@192.168.56.10
```

### Specify private key

```
ssh -i C:\Users\Sohan\.ssh\id_ed25519 student@192.168.56.10
```

### Verbose troubleshooting

```
ssh -v student@192.168.56.10
```

More verbose:

```
ssh -vv student@192.168.56.10
```

Maximum debugging:

```
ssh -vvv student@192.168.56.10
```