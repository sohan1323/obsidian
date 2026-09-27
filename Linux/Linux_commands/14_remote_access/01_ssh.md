
---
`ssh` provides secure remote access to another system.

It creates an encrypted connection over the network.

### Syntax

```
ssh [OPTIONS] USER@HOST
```

### Basic connection

```
ssh user@192.168.1.10
```

Using a hostname:

```
ssh user@server.example.com
```

Specify a port:

```
ssh -p 2222 user@192.168.1.10
```

### Important options

|Option|Purpose|
|---|---|
|`-p PORT`|SSH server port|
|`-i FILE`|Private key to use|
|`-v`|Verbose debugging|
|`-vv`|More debugging|
|`-vvv`|Maximum SSH debugging|
|`-l USER`|Specify username|
|`-o OPTION=VALUE`|Set SSH configuration option|
|`-L`|Local port forwarding|
|`-R`|Remote port forwarding|
|`-D`|Dynamic SOCKS proxy|
|`-N`|Don't execute remote command|
|`-f`|Background after authentication|
|`-T`|Disable pseudo-terminal|
|`-t`|Force pseudo-terminal|

---

### Execute a command remotely

```
ssh user@192.168.1.10 "uname -a"
```

Multiple commands:

```
ssh user@192.168.1.10 "whoami; id; hostname"
```

### Use a private key

```
ssh -i ~/.ssh/id_ed25519 user@192.168.1.10
```

### Debug connection

```
ssh -vvv user@192.168.1.10
```

This is useful when troubleshooting:

- authentication
- key exchange
- host keys
- connection failures