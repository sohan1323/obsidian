
---
Writes a message to the system logging facility.

### Syntax

```
logger [OPTIONS] MESSAGE
```

### Basic example

```
logger "Test security event"
```

The message can then appear in the system journal/logging system.

### Specify a tag

```
logger -t myscript "Backup completed"
```

Then search:

```
journalctl -t myscript
```

### Specify priority

```
logger -p user.warning "Test warning"
```

Format:

```
FACILITY.PRIORITY
```

Examples:

```
logger -p user.info "Information"
logger -p user.warning "Warning"
logger -p user.err "Error"
```

### Practical use

Shell scripts can use `logger` to send events to the system logging infrastructure.