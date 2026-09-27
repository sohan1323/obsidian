
---
**Purpose:** Send a signal to processes based on their name.

### Syntax

```
killall [OPTIONS] NAME
```

Example:

```
killall firefox
```

Send SIGTERM to matching Firefox processes.

Force:

```
sudo killall -9 firefox
```

### Important options

|Option|Meaning|
|---|---|
|`-9`|SIGKILL|
|`-i`|Interactive|
|`-u USER`|Only processes owned by USER|
|`-v`|Verbose|
|`-q`|Quiet|
|`-w`|Wait for termination|

### Warning

Be careful with process names.

For example:

```
killall python
```

could terminate **multiple Python processes**.