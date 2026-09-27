
---
**Purpose:** Send output to both the terminal and a file.

### Syntax

```
COMMAND | tee [OPTIONS] FILE
```

### Important options

|Option|Meaning|
|---|---|
|`-a`|Append instead of overwrite|
|`-i`|Ignore interrupts|

### Example

```
echo "hello" | tee output.txt
```

You see:

```
hello
```

and `output.txt` contains:

```
hello
```

Append:

```
echo "another line" | tee -a output.txt
```

### Practical use

Save command output while still seeing it:

```
nmap 192.168.1.1 | tee scan.txt
```

This is extremely useful during pentesting.