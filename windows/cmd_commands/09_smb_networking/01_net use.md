
---
`net use` manages connections to shared network resources.

### Basic syntax

```
net use
```

Displays current network connections.

```
net use \\SERVER\Share
```

Connects to a network share.

---

## `net use \\SERVER\Share`

Example:

```
net use \\192.168.1.20\Shared
```

This connects to the SMB share.

If authentication is required:

```
net use \\192.168.1.20\Shared /user:LAB\alice
```

You will normally be prompted for the password.

---

## Map a network share to a drive

```
net use Z: \\SERVER\Shared
```

Now:

```
Z:
```

can be used like a local drive.

Example:

```
net use Z: \\192.168.1.20\Shared
```

---

## `/user:`

Specifies the account used for authentication.

```
net use Z: \\SERVER\Shared /user:LAB\alice
```

Local account:

```
net use Z: \\SERVER\Shared /user:SERVER01\alice
```

Domain account:

```
net use Z: \\SERVER\Shared /user:DOMAIN\alice
```

---

## `/persistent:`

Controls whether the connection is restored at sign-in.

### Persistent

```
net use Z: \\SERVER\Shared /persistent:yes
```

### Not persistent

```
net use Z: \\SERVER\Shared /persistent:no
```

---

## `/delete`

Disconnects a network connection.

```
net use Z: /delete
```

Disconnect a UNC connection:

```
net use \\SERVER\Shared /delete
```

Disconnect all network connections:

```
net use * /delete
```

Be careful with the last command because it can remove multiple existing connections.