
---
Displays or changes the system time.

### Syntax

```
time [/t]
```

### Arguments

|Argument|Meaning|
|---|---|
|`/t`|Display current time without prompting|

### Examples

```
time /t
```

Possible output:

```
10:45
```

Without `/t`:

```
time
```

CMD can prompt for a new time.

### Script usage

```
echo %TIME%
```