
---
**Purpose:** Run a command so it can continue after the terminal/session closes.

### Syntax

```
nohup COMMAND [ARGUMENTS] &
```

Example:

```
nohup ./server.sh &
```

By default, output may be written to:

```
nohup.out
```

Redirect output explicitly:

```
nohup ./server.sh > server.log 2>&1 &
```

### Meaning of:

```
> server.log
```

stdout → file.

```
2>&1
```

stderr → same destination as stdout.

```
&
```

run in background.

### Practical use

Long-running commands:

```
nohup python3 server.py > server.log 2>&1 &
```