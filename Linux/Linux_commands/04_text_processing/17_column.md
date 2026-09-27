
---
**Purpose:** Format text into aligned columns.

### Syntax

```
column [OPTIONS]
```

Example:

```
cat data.txt | column -t
```

If:

```
Alice 20 Security
Bob 21 Development
Charlie 22 Networking
```

it can format it as aligned columns.

### Important options

|Option|Meaning|
|---|---|
|`-t`|Create a table|
|`-s CHAR`|Specify input separator|
|`-N names`|Specify column names|

Example:

```
cat /etc/passwd | column -t -s ':'
```