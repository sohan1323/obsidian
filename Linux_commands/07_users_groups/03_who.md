
---
**Purpose:** Show users currently logged into the system.

### Syntax

```
who [OPTIONS]
```

### Example

```
who
```

Possible output:

```
sohan    tty2         2026-09-22 14:10
alice    pts/0        2026-09-22 14:30 (192.168.1.20)
```

Information can include:

- Username
- Terminal
- Login time
- Remote host

### Important options

|Option|Meaning|
|---|---|
|`-H`|Show headers|
|`-q`|Show usernames and count|
|`-b`|Show last system boot|
|`-r`|Show current runlevel|
|`-a`|Show additional information|

Example:

```
who -b
```

Shows when the system last booted.