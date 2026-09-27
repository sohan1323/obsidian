
---
**Purpose:** Displays previously executed shell commands.

### Syntax

```bash
history [N]
```

### Important options

|Option|Meaning|
|---|---|
|`-c`|Clear history|
|`-d OFFSET`|Delete a history entry|
|`-w`|Write current history to history file|
|`-r`|Read history file|

### Examples

Show history:

```bash
history
```

Show last 10 commands:

```bash
history 10
```

Search previous commands:

```bash
history | grep ssh
```

Example:

```
 102  ssh user@192.168.1.10
 108  ssh user@server
```

Clear current shell history:

```bash
history -c
```

### Very useful Bash feature

Press:

```
Ctrl + R
```

Then type:

```
ssh
```

Bash searches your previous commands containing `ssh`.