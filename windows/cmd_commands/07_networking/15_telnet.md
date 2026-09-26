
---
Provides a basic TCP client.

It may not be installed/enabled by default on modern Windows.

### Syntax

```
telnet hostname port
```

Example:

```
telnet 192.168.1.10 80
```

If a TCP connection succeeds, you may see a blank or protocol-specific response.

For basic port connectivity testing on modern Windows, `Test-NetConnection` in PowerShell is generally more useful.