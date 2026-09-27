
---
Downloads files from HTTP, HTTPS, and FTP servers.

### Syntax

```
wget [OPTIONS] URL
```

### Important options

|Option|Purpose|
|---|---|
|`-O FILE`|Save with specified filename|
|`-c`|Continue interrupted download|
|`-q`|Quiet|
|`-nv`|Less verbose|
|`-r`|Recursive download|
|`-np`|Don't ascend to parent directory|
|`--limit-rate`|Limit download rate|

### Examples

Download:

```
wget https://example.com/file.zip
```

Specify output:

```
wget -O tool.zip https://example.com/file.zip
```

Continue:

```
wget -c https://example.com/large.iso
```

### Practical use

Download a file:

```
wget https://example.com/file.txt
```