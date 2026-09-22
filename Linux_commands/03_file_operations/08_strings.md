
---
**Purpose:** Extract readable strings from binary or other files.

### Syntax

```
strings [OPTION] FILE
```

### Important options

|Option|Meaning|
|---|---|
|`-n NUMBER`|Minimum string length|
|`-a`|Scan entire file|
|`-t FORMAT`|Show offset|
|`-e ENCODING`|Character encoding|

### Examples

```
strings program
```

Find strings of at least 10 characters:

```
strings -n 10 program
```

Show offsets:

```
strings -t x program
```

### Practical cybersecurity use

Suppose you have:

```
suspicious_binary
```

You can run:

```
strings suspicious_binary
```

You might discover readable content such as:

```
http://example.com
password
config
API_KEY
/tmp/payload
```

This doesn't mean every discovered string is actually used by the program, but it is useful for initial binary inspection.