
---
Displays, creates, modifies, and removes SMB shares.

### List shares

```
net share
```

You may see:

```
Share name
---------
ADMIN$
C$
IPC$
Users
```

Some are administrative/system shares.

---

## Create a share

```
net share Lab=C:\CLI-Lab
```

This shares:

```
C:\CLI-Lab
```

under the share name:

```
Lab
```

Remote clients can access it as:

```
\\ComputerName\Lab
```

---

## Delete a share

```
net share Lab /delete
```

This removes the share definition; it does not delete the underlying directory.

---

## Display a specific share

```
net share Lab
```