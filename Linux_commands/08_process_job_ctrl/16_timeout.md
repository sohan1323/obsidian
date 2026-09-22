
---
**Purpose:** Run a command for a limited amount of time.

### Syntax

```
timeout [OPTIONS] DURATION COMMAND
```

Example:

```
timeout 10s ping 8.8.8.8
```

The command is allowed to run for 10 seconds.

### Duration suffixes

|Suffix|Meaning|
|---|---|
|`s`|seconds|
|`m`|minutes|
|`h`|hours|
|`d`|days|

Examples:

```
timeout 30s command
```

```
timeout 5m command
```

### Send a specific signal

```
timeout -s KILL 30s command
```

### Practical use

Prevent a command from running indefinitely:

```
timeout 30s ./scan.sh
```