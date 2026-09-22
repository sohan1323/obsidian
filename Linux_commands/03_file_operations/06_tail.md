
---
**Purpose:** Display the end of a file.

### Syntax

```
tail [OPTION]... [FILE]...
```

By default, it displays the last **10 lines**.

### Important options

|Option|Meaning|
|---|---|
|`-n NUMBER`|Show NUMBER lines|
|`-c NUMBER`|Show NUMBER bytes|
|`-f`|Follow file as it grows|
|`-F`|Follow file and handle file replacement|
|`-q`|Don't print filenames|
|`-v`|Always print filenames|

### Examples

Last 10 lines:

```
tail file.txt
```

Last 5 lines:

```
tail -n 5 file.txt
```

Last 50 lines:

```
tail -n 50 file.txt
```

### Extremely important: `-f`

```
tail -f /var/log/auth.log
```

This continuously displays new lines added to the file.

Press:

```
Ctrl + C
```

to stop.

### Practical cybersecurity use

Monitor a log in real time:

```
tail -f /var/log/auth.log
```

Then, in another terminal, perform an action that generates a log entry.

You can watch the event appear.