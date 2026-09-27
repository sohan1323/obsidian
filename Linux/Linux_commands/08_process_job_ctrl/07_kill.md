
---
**Purpose:** Send a signal to a process.

Despite its name, `kill` doesn't necessarily mean "terminate immediately."

### Syntax

```
kill [OPTIONS] PID
```

Example:

```
kill 1234
```

By default, this sends:

```
SIGTERM (15)
```

which politely requests termination.

---

## Important signals

|Signal|Number|Meaning|
|---|---|---|
|`SIGHUP`|1|Hangup|
|`SIGINT`|2|Interrupt|
|`SIGQUIT`|3|Quit|
|`SIGKILL`|9|Forcefully terminate|
|`SIGTERM`|15|Request termination|
|`SIGSTOP`|19|Stop process|
|`SIGCONT`|18|Continue stopped process|

List signals:

```
kill -l
```

---

## Terminate normally

```
kill 1234
```

Explicitly send SIGTERM:

```
kill -TERM 1234
```

or:

```
kill -15 1234
```

Force termination:

```
kill -9 1234
```

Stop:

```
kill -STOP 1234
```

Continue:

```
kill -CONT 1234
```

### Important

Prefer:

```
kill PID
```

before:

```
kill -9 PID
```

`SIGTERM` gives the application an opportunity to clean up resources. `SIGKILL` cannot be caught or handled by the target process.