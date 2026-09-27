
---
### Purpose

Displays or changes the system's hostname.

### Syntax

```
hostname [OPTION] [NAME]
```

### Important options

|Option|Purpose|
|---|---|
|`-s`|Short hostname|
|`-f`|Fully qualified hostname|
|`-I`|Display IP addresses|
|`-i`|Display hostname's IP address|
|`-d`|DNS domain name|

### Examples

```
hostname
```

```
kali
```

Get IP addresses:

```
hostname -I
```

Get FQDN:

```
hostname -f
```

### Practical use

During system enumeration:

```
hostname
hostname -I
```