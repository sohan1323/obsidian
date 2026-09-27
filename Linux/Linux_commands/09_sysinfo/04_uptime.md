
---
### Purpose

Shows how long the system has been running and system load averages.

### Syntax

```
uptime [OPTION]
```

### Important options

|Option|Purpose|
|---|---|
|`-p`|Pretty uptime|
|`-s`|System start time|

### Examples

```
uptime
```

Example:

```
20:30:15 up 3 days, 4:22, 2 users, load average: 0.20, 0.15, 0.10
```

```
uptime -p
```

```
up 3 days, 4 hours, 22 minutes
```

```
uptime -s
```

Shows when the system booted.

### Practical use

Check whether a machine has been running for a long time:

```
uptime
```