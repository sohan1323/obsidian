
---
Queries DNS servers.

### Syntax

```
nslookup [options] [hostname] [DNS-server]
```

### Basic

```
nslookup google.com
```

Example:

```
Server:  dns.example
Address:  192.168.1.1

Non-authoritative answer:
Name:    google.com
Addresses: ...
```

---

## Query A record

```
nslookup -type=A example.com
```

---

## Query AAAA

```
nslookup -type=AAAA example.com
```

---

## Query MX

```
nslookup -type=MX example.com
```

Useful for mail infrastructure.

---

## Query NS

```
nslookup -type=NS example.com
```

---

## Query TXT

```
nslookup -type=TXT example.com
```

---

## Query SOA

```
nslookup -type=SOA example.com
```

---

## Use a specific DNS server

```
nslookup example.com 8.8.8.8
```

This asks Google's public DNS server.

---

## Reverse lookup

```
nslookup 8.8.8.8
```

Attempts reverse DNS resolution.

---

## Interactive mode

Run:

```
nslookup
```

You'll enter:

```
>
```

Then:

```
> server 8.8.8.8
> set type=MX
> example.com
```

Exit:

```
> exit
```