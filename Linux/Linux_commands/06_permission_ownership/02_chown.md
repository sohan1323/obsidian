
---
**Purpose:** Change file ownership.

### Syntax

```
chown [OPTION] USER[:GROUP] FILE...
```

### Examples

Change owner:

```
sudo chown alice file.txt
```

Change owner and group:

```
sudo chown alice:developers file.txt
```

Change only group:

```
sudo chown :developers file.txt
```

Recursive:

```
sudo chown -R alice:developers project/
```

### Important options

|Option|Meaning|
|---|---|
|`-R`|Recursive|
|`-v`|Verbose|
|`-c`|Report changes|
|`-f`|Suppress errors|
|`-h`|Affect symbolic link itself|

---

## Practical example

Suppose you create a file as `root`:

```
sudo touch /tmp/test.txt
```

Check:

```
ls -l /tmp/test.txt
```

It might show:

```
root root
```

Change owner:

```
sudo chown $USER:$USER /tmp/test.txt
```

Check again:

```
ls -l /tmp/test.txt
```