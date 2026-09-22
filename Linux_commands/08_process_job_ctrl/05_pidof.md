
---
**Purpose:** Find the PID of a running program.

### Syntax

```
pidof [OPTIONS] PROGRAM
```

Example:

```
pidof sshd
```

Output:

```
721 1082
```

### Important options

|Option|Meaning|
|---|---|
|`-s`|Single PID|
|`-c`|Only processes in same root directory|
|`-x`|Include scripts|

### Example

```
pidof nginx
```