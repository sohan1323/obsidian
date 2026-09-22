
---
Performs detailed DNS queries.

It is one of the most important DNS troubleshooting and security-enumeration tools.

### Syntax

```
dig [@DNS_SERVER] [DOMAIN] [TYPE]
```

### Basic query

```
dig example.com
```

The response contains:

```
QUESTION SECTION
ANSWER SECTION
AUTHORITY SECTION
ADDITIONAL SECTION
```

### Query specific record types

A record:

```
dig example.com A
```

AAAA:

```
dig example.com AAAA
```

MX:

```
dig example.com MX
```

NS:

```
dig example.com NS
```

TXT:

```
dig example.com TXT
```

CNAME:

```
dig www.example.com CNAME
```

SOA:

```
dig example.com SOA
```

### Short output

```
dig +short example.com
```

### Query a specific DNS server

```
dig @8.8.8.8 example.com
```

```
dig @1.1.1.1 example.com
```

### Reverse DNS

```
dig -x 8.8.8.8
```

### Trace DNS resolution

```
dig +trace example.com
```

This follows the DNS hierarchy:

```
Root
 ↓
TLD
 ↓
Authoritative DNS
 ↓
Domain
```

### Practical security use

Enumerate common DNS records:

```
dig example.com A
dig example.com MX
dig example.com NS
dig example.com TXT
```