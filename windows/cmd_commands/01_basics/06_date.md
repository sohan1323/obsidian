
---
Displays or changes the system date.

### Syntax

```
date [/t]
```

### Arguments

|Argument|Meaning|
|---|---|
|`/t`|Display date without asking to change it|

### Examples

```
date
```

Displays the current date and may prompt for a new date.

Use:

```
date /t
```

to simply display it.

### Practical use

In scripts:

```
echo %DATE%
```

is generally more convenient.