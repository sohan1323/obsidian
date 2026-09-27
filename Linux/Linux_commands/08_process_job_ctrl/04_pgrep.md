
---
**Purpose:** Find process IDs based on process name or other attributes.

### Syntax

```
pgrep [OPTIONS] PATTERN
```

### Example

```
pgrep ssh
```

Output:

```
721
1092
```

These are PIDs matching `ssh`.

### Show PID and command

```
pgrep -a ssh
```

Possible:

```
721 /usr/sbin/sshd
1092 ssh user@server
```

### Search exact process name

```
pgrep -x sshd
```

### Search by user

```
pgrep -u alice
```

### Search by UID

```
pgrep -u 1000
```

### Important options

|Option|Meaning|
|---|---|
|`-a`|Show PID and full command|
|`-f`|Match full command line|
|`-x`|Exact process name|
|`-u USER`|Processes owned by user|
|`-n`|Newest matching process|
|`-o`|Oldest matching process|
|`-c`|Count matching processes|

### Example

Count SSH processes:

```
pgrep -c ssh
```