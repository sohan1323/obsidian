
---
Connects to, disconnects from, or displays network resources and SMB shares.

### Syntax

```
net use
net use \\Computer\Share
net use X: \\Computer\Share
net use X: /delete
```

---

## Display current connections

```
net use
```

---

## Connect to an SMB share

```
net use Z: \\SERVER01\Shared
```

Now:

```
dir Z:\
```

can access the share through drive `Z:`.

---

## Disconnect

```
net use Z: /delete
```

---

## Disconnect all network connections

```
net use * /delete
```

CMD will normally ask for confirmation.

---

## Persistent connection

```
net use Z: \\SERVER01\Shared /persistent:yes
```

This can reconnect the mapping in future sessions.

Disable persistence:

```
net use Z: \\SERVER01\Shared /persistent:no
```