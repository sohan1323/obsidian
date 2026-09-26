
---
Pauses execution for a specified number of seconds.

### Syntax

```
timeout /t seconds [/nobreak]
```

### Basic

```
timeout /t 5
```

Waits five seconds.

### `/nobreak`

Prevents a keypress from skipping the timeout.

```
timeout /t 10 /nobreak
```

### Useful in scripts

```
echo Starting service...
timeout /t 3
echo Continuing...
```