
---
Older networking statistics and socket utility.

Usually provided by the `net-tools` package.

### Examples

```
netstat -tuln
```

Listening TCP/UDP ports.

```
sudo netstat -tulnp
```

Show processes.

```
netstat -rn
```

Routing table.

### Modern replacement

Instead of:

```
netstat -tulnp
```

use:

```
sudo ss -lntup
```