
---
Performs DNS queries.

It is older than `dig` but still widely encountered.

### Syntax

```
nslookup [DOMAIN]
```

### Examples

```
nslookup example.com
```

Specify DNS server:

```
nslookup example.com 8.8.8.8
```

Reverse lookup:

```
nslookup 8.8.8.8
```

Interactive mode:

```
nslookup
```

Then:

```
> server 8.8.8.8
> example.com
```

### Practical use

Quick DNS testing:

```
nslookup example.com
```