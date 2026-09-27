
---
**Purpose:** Display processes in a parent-child tree.

### Syntax

```
pstree [OPTIONS] [PID]
```

Example:

```
pstree
```

Possible:

```
systemd
├─sshd
│ └─sshd
│   └─bash
│     └─python
├─cron
└─NetworkManager
```

### Show PIDs

```
pstree -p
```

Show a specific user's processes:

```
pstree alice
```

### Important options

|Option|Meaning|
|---|---|
|`-p`|Show PIDs|
|`-u`|Show transitions in UID|
|`-a`|Show command arguments|
|`-s PID`|Show ancestors|
|`-T`|Don't show threads|

### Practical use

Understanding process relationships:

```
pstree -p
```

This is particularly useful when investigating which process launched another process.