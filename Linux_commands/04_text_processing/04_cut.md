
---
**Purpose:** Extract specific columns/characters from lines.

### Syntax

```
cut OPTION... [FILE]
```

### Important options

|Option|Meaning|
|---|---|
|`-d DELIMITER`|Specify field delimiter|
|`-f LIST`|Select fields|
|`-c LIST`|Select characters|
|`-b LIST`|Select bytes|
|`--complement`|Select everything except specified fields|

---

## Field extraction

Suppose:

```
user:x:1000:1000:John:/home/user:/bin/bash
```

Fields are separated by `:`.

Extract username:

```
cut -d ':' -f 1 /etc/passwd
```

Extract username and shell:

```
cut -d ':' -f 1,7 /etc/passwd
```

Extract fields 1 through 3:

```
cut -d ':' -f 1-3 /etc/passwd
```

Extract everything except field 1:

```
cut -d ':' --complement -f 1 /etc/passwd
```

### Character extraction

```
cut -c 1-5 file.txt
```

Displays characters 1 through 5.

```
cut -c 1,3,5 file.txt
```

Displays characters 1, 3 and 5.

### Practical use

Extract usernames:

```
cut -d ':' -f 1 /etc/passwd
```

Extract IP addresses from structured output when appropriate:

```
ip -4 addr | grep inet | cut -d ' ' -f 6
```