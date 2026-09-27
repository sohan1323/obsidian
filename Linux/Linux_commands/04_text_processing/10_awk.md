
---
**Purpose:** Powerful text-processing language particularly useful for **field extraction, filtering, calculations, and reporting**.

### Syntax

```
awk 'PATTERN { ACTION }' FILE
```

Consider:

```
john 1000 admin
alice 1001 user
bob 1002 user
```

### Print first field

```
awk '{print $1}' file.txt
```

Output:

```
john
alice
bob
```

Print second field:

```
awk '{print $2}' file.txt
```

Print first and third:

```
awk '{print $1, $3}' file.txt
```

### Specify delimiter

For `/etc/passwd`:

```
awk -F ':' '{print $1}' /etc/passwd
```

Print username and shell:

```
awk -F ':' '{print $1, $7}' /etc/passwd
```

### Filtering

```
awk '$2 > 1000 {print $1}' file.txt
```

Print users whose second field is greater than 1000.

### Built-in variables

|Variable|Meaning|
|---|---|
|`$0`|Entire line|
|`$1`|First field|
|`$2`|Second field|
|`NF`|Number of fields|
|`NR`|Current record/line number|
|`FS`|Input field separator|
|`OFS`|Output field separator|

Example:

```
awk '{print NR, $0}' file.txt
```

Adds line numbers.

Print number of fields:

```
awk '{print NF}' file.txt
```

### Practical cybersecurity use

List users whose shell is `/bin/bash`:

```
awk -F ':' '$7 == "/bin/bash" {print $1}' /etc/passwd
```

Extract network information:

```
ip addr | awk '/inet / {print $2}'
```