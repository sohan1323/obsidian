
---
Simple DNS lookup utility.

### Syntax

```
host [OPTIONS] DOMAIN
```

### Examples

```
host example.com
```

IPv4:

```
host -t A example.com
```

IPv6:

```
host -t AAAA example.com
```

MX:

```
host -t MX example.com
```

NS:

```
host -t NS example.com
```

TXT:

```
host -t TXT example.com
```

Reverse lookup:

```
host 8.8.8.8
```

### Practical use

Quick DNS enumeration:

```
host -t MX example.com
host -t NS example.com
host -t TXT example.com
```