
---
**Purpose:** Send signals to processes based on a pattern.

### Syntax

```
pkill [OPTIONS] PATTERN
```

Example:

```
pkill firefox
```

### Exact name

```
pkill -x firefox
```

### By user

```
sudo pkill -u alice
```

### Send specific signal

```
pkill -TERM firefox
```

Force:

```
pkill -KILL firefox
```

### Match full command line

```
pkill -f "python app.py"
```

### Important options

|Option|Meaning|
|---|---|
|`-f`|Match full command line|
|`-x`|Exact match|
|`-u USER`|Match user|
|`-TERM`|Send SIGTERM|
|`-KILL`|Send SIGKILL|

### `pgrep` vs `pkill`

```
pgrep ssh
```

**Find** matching processes.

```
pkill ssh
```

**Signal** matching processes.