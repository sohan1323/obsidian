
---
`nslookup` (**Name Server Lookup**) is a command-line tool for querying DNS servers.

In pentesting, it is useful for:

- DNS reconnaissance
- Finding IP addresses
- Finding nameservers
- Finding mail servers
- Reverse DNS
- Querying specific DNS servers
- Basic DNS troubleshooting
- Comparing DNS responses from different resolvers

It overlaps heavily with `dig`, but `nslookup` is generally simpler and is also available by default on many Windows systems.

---

# 1. Installation

### Kali / Debian / Ubuntu

Usually available through the `dnsutils` package:

```
sudo apt update
sudo apt install dnsutils
```

Check:

```
nslookup -version
```

or:

```
which nslookup
```

### Windows

`nslookup` is normally already included.

Open:

```
Command Prompt
```

and run:

```
nslookup
```

---

# 2. Basic Syntax

There are two common forms.

### Non-interactive

```
nslookup [OPTIONS] DOMAIN [DNS_SERVER]
```

Example:

```
nslookup example.com
```

### Interactive

```
nslookup
```

Then:

```
> example.com
```

---

# 3. Basic Domain Lookup

```
nslookup example.com
```

Typical output:

```
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   example.com
Address: 93.184.216.34
```

This tells you:

```
DNS resolver
     ↓
example.com
     ↓
IPv4 address
```

---

# 4. Understand the Output

Example:

```
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:           example.com
Address:        93.184.216.34
```

### `Server`

```
192.168.1.1
```

The DNS resolver that answered your query.

### `#53`

DNS normally uses:

```
UDP/TCP 53
```

### `Non-authoritative answer`

The response came from a recursive resolver/cache rather than directly from the domain's authoritative nameserver.

### `Name`

The queried hostname.

### `Address`

The resulting IP address.

---

# 5. Query an A Record

```
nslookup -type=A example.com
```

or:

```
nslookup -query=A example.com
```

Example:

```
Name:    example.com
Address: 93.184.216.34
```

---

# 6. Query AAAA

For IPv6:

```
nslookup -type=AAAA example.com
```

or:

```
nslookup -query=AAAA example.com
```

---

# 7. Query MX Records

MX records identify mail servers.

```
nslookup -type=MX example.com
```

Example:

```
example.com    MX preference = 10, mail exchanger = mail.example.com
```

The preference value is the mail-server priority.

---

# 8. Query NS Records

Find authoritative nameservers:

```
nslookup -type=NS example.com
```

Example:

```
example.com    nameserver = ns1.example.com
example.com    nameserver = ns2.example.com
```

This is an important first step in DNS reconnaissance.

---

# 9. Query TXT Records

```
nslookup -type=TXT example.com
```

This can expose records such as SPF and domain-verification information.

For example:

```
"v=spf1 include:_spf.example.com ~all"
```

---

# 10. Query SOA

```
nslookup -type=SOA example.com
```

The SOA record provides zone-authority information.

You may see:

```
primary name server
responsible mailbox
serial number
refresh
retry
expire
minimum TTL
```

---

# 11. Query CNAME

```
nslookup -type=CNAME www.example.com
```

Example:

```
www.example.com    canonical name = web.example.net
```

This is useful when investigating where a hostname ultimately points.

---

# 12. Reverse DNS

To perform a reverse lookup:

```
nslookup 8.8.8.8
```

You may receive:

```
Name:    dns.google
Address: 8.8.8.8
```

This performs a PTR-style reverse lookup.

You can also use the explicit form:

```
nslookup -type=PTR 8.8.8.8
```

Conceptually:

```
IP address
    ↓
PTR
    ↓
hostname
```

---

# 13. Query a Specific DNS Server

This is extremely useful.

Syntax:

```
nslookup DOMAIN DNS_SERVER
```

Example:

```
nslookup example.com 8.8.8.8
```

Here:

```
example.com
    ↓
query
    ↓
8.8.8.8
    ↓
Google Public DNS
```

Another:

```
nslookup example.com 1.1.1.1
```

This lets you compare results from different resolvers.

---

# 14. Query Specific Record + Specific DNS Server

You can combine them.

```
nslookup -type=MX example.com 8.8.8.8
```

Another:

```
nslookup -type=NS example.com 1.1.1.1
```

Another:

```
nslookup -type=TXT example.com 8.8.8.8
```

General pattern:

```
nslookup -type=RECORD DOMAIN DNS_SERVER
```

---

# 15. `-type`

The most important option.

Syntax:

```
nslookup -type=TYPE DOMAIN
```

Examples:

```
nslookup -type=A example.com
```

```
nslookup -type=AAAA example.com
```

```
nslookup -type=MX example.com
```

```
nslookup -type=NS example.com
```

```
nslookup -type=TXT example.com
```

```
nslookup -type=SOA example.com
```

```
nslookup -type=CNAME www.example.com
```

---

# 16. `-query`

`-query` is an alternative way of specifying the record type.

```
nslookup -query=MX example.com
```

Equivalent:

```
nslookup -type=MX example.com
```

---

# 17. Interactive Mode

Start:

```
nslookup
```

You'll get:

```
>
```

Now enter:

```
> example.com
```

You can continue issuing queries without restarting the program.

---

# 18. Set Record Type in Interactive Mode

Start:

```
nslookup
```

Then:

```
> set type=MX
> example.com
```

Now you're asking for MX records.

Change to NS:

```
> set type=NS
> example.com
```

Change to TXT:

```
> set type=TXT
> example.com
```

Change to A:

```
> set type=A
> example.com
```

---

# 19. Change DNS Server in Interactive Mode

Start:

```
nslookup
```

You'll see something similar to:

```
Default Server: 192.168.1.1
Address: 192.168.1.1
```

Change it:

```
> server 8.8.8.8
```

Now:

```
> example.com
```

The query will be sent to:

```
8.8.8.8
```

Another:

```
> server 1.1.1.1
```

---

# 20. Interactive DNS Recon Example

Start:

```
nslookup
```

Then:

```
> server 8.8.8.8
> set type=NS
> example.com
```

Then:

```
> set type=MX
> example.com
```

Then:

```
> set type=TXT
> example.com
```

Then:

```
> set type=SOA
> example.com
```

This lets you investigate several record types using one session.

Exit:

```
> exit
```

---

# 21. Find Nameservers

```
nslookup -type=NS example.com
```

Suppose you get:

```
ns1.example.com
ns2.example.com
```

You can then investigate those nameservers:

```
nslookup ns1.example.com
```

```
nslookup ns2.example.com
```

And with `dig`:

```
dig ns1.example.com A
```

---

# 22. Find Mail Servers

```
nslookup -type=MX example.com
```

Suppose:

```
mail.example.com
```

Then:

```
nslookup mail.example.com
```

This can give you its IP address.

---

# 23. Find TXT/SPF Information

```
nslookup -type=TXT example.com
```

Look for:

```
v=spf1
```

For example:

```
"v=spf1 include:_spf.google.com ~all"
```

This can identify external mail providers authorized by the domain.

---

# 24. DMARC

DMARC normally lives at:

```
_dmarc.example.com
```

Query:

```
nslookup -type=TXT _dmarc.example.com
```

Example:

```
"v=DMARC1; p=reject; ..."
```

This is useful when assessing email-security configuration.

---

# 25. CNAME Reconnaissance

Suppose you find:

```
dev.example.com
```

Query:

```
nslookup -type=CNAME dev.example.com
```

If it returns:

```
dev.example.com canonical name = example.hosting-provider.net
```

you've discovered that the subdomain points to another hostname.

You can then resolve it:

```
nslookup example.hosting-provider.net
```

---

# 26. Reverse DNS

Given:

```
203.0.113.10
```

run:

```
nslookup 203.0.113.10
```

or:

```
nslookup -type=PTR 203.0.113.10
```

If a PTR exists, you might receive:

```
10.113.0.203.in-addr.arpa
    name = host.example.com
```

Reverse DNS can provide useful host naming information, but many IPs don't have meaningful PTR records.

---

# 27. Query Your Local DNS Resolver

Simply:

```
nslookup example.com
```

The output shows:

```
Server:
Address:
```

This tells you which resolver your system is currently using.

On Linux, this can be useful when troubleshooting DNS configuration.

---

# 28. Compare DNS Resolvers

Query resolver 1:

```
nslookup example.com 8.8.8.8
```

Query resolver 2:

```
nslookup example.com 1.1.1.1
```

Compare:

```
8.8.8.8
    ↓
response

1.1.1.1
    ↓
response
```

Differences can sometimes indicate caching or DNS propagation differences.

---

# 29. Query Authoritative Server Directly

First:

```
nslookup -type=NS example.com
```

Suppose:

```
ns1.example.com
```

Then:

```
nslookup example.com ns1.example.com
```

Now you're asking that DNS server directly.

This is useful for distinguishing:

```
Recursive resolver
        vs
Authoritative server
```

---

# 30. Zone Transfer — AXFR

`nslookup` can also request a zone transfer in interactive mode.

Start:

```
nslookup
```

Set the server:

```
> server ns1.example.com
```

Then:

```
> ls -d example.com
```

This attempts to list DNS records from the zone.

An authorized DNS security test may use this to determine whether an authoritative server improperly permits zone transfers.

If the server is correctly configured, you will generally receive an error/refusal.

### Important

Do this only against DNS infrastructure you are authorized to test.

For modern pentesting, `dig` is generally more convenient for explicit AXFR testing:

```
dig @ns1.example.com example.com AXFR
```

---

# 31. Query SRV Records

SRV records identify services.

Example:

```
nslookup -type=SRV _sip._tcp.example.com
```

Another common pattern:

```
nslookup -type=SRV _ldap._tcp.example.com
```

This can be particularly useful during **authorized Active Directory/DNS reconnaissance**, where SRV records can identify domain services.

---

# 32. Query CAA Records

CAA records specify which certificate authorities are authorized to issue certificates for a domain.

```
nslookup -type=CAA example.com
```

Example:

```
example.com
    CAA 0 issue "letsencrypt.org"
```

Useful during domain/certificate-security assessment.

---

# 33. Query DNSSEC Records

You can query:

```
nslookup -type=DNSKEY example.com
```

or:

```
nslookup -type=DS example.com
```

or:

```
nslookup -type=RRSIG example.com
```

These can help inspect DNSSEC configuration.

---

# 34. Common DNS Record Types

Memorize these:

|Type|Purpose|
|---|---|
|`A`|IPv4 address|
|`AAAA`|IPv6 address|
|`CNAME`|Alias|
|`MX`|Mail server|
|`NS`|Nameserver|
|`TXT`|Text/configuration|
|`SOA`|Zone authority|
|`PTR`|Reverse DNS|
|`SRV`|Service location|
|`CAA`|Certificate authority authorization|
|`DS`|DNSSEC delegation|
|`DNSKEY`|DNSSEC key|
|`RRSIG`|DNSSEC signature|
|`AXFR`|Zone transfer|

---

# 35. `nslookup` vs `dig`

You should know both.

|Feature|`nslookup`|`dig`|
|---|---|---|
|Basic DNS lookup|✅|✅|
|A/AAAA/MX/NS/TXT|✅|✅|
|Reverse DNS|✅|✅|
|Specific DNS server|✅|✅|
|Interactive mode|✅|✅|
|Detailed DNS response|Limited|Excellent|
|DNS tracing|Limited|✅ `+trace`|
|Clean scripting output|Moderate|Excellent|
|AXFR testing|✅|✅|
|DNS troubleshooting|Good|Excellent|
|Windows availability|✅|Usually not default|
|Pentesting preference|Useful|Usually preferred|

A practical rule:

```
nslookup
   ↓
Simple / quick DNS queries

dig
   ↓
Detailed DNS reconnaissance + troubleshooting
```

---

# 36. `nslookup` + `whois` Workflow

For an authorized target:

### 1. WHOIS

```
whois example.com
```

### 2. A record

```
nslookup example.com
```

### 3. Nameservers

```
nslookup -type=NS example.com
```

### 4. Mail servers

```
nslookup -type=MX example.com
```

### 5. TXT

```
nslookup -type=TXT example.com
```

### 6. Reverse DNS

```
nslookup <IP>
```

---

# 37. `nslookup` + `dig` Workflow

You can use `nslookup` for quick discovery and `dig` for deeper inspection.

```
               DOMAIN
                  │
                  ▼
             nslookup
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
        A         NS        MX
        │         │         │
        ▼         ▼         ▼
       IP      DNS servers  Mail
        │
        ▼
   nslookup -type=PTR
        │
        ▼
     hostname
```

Then use:

```
dig example.com +trace
```

for detailed DNS delegation analysis.

---

# 38. Practical Recon Script

For a single authorized domain:

```
#!/bin/bash

domain="$1"

echo "===== A ====="
nslookup -type=A "$domain"

echo
echo "===== AAAA ====="
nslookup -type=AAAA "$domain"

echo
echo "===== NS ====="
nslookup -type=NS "$domain"

echo
echo "===== MX ====="
nslookup -type=MX "$domain"

echo
echo "===== TXT ====="
nslookup -type=TXT "$domain"

echo
echo "===== SOA ====="
nslookup -type=SOA "$domain"
```

Run:

```
chmod +x dns-recon.sh
```

Then:

```
./dns-recon.sh example.com
```

---

# 39. Query Multiple Domains

Create:

```
domains.txt
```

Example:

```
example.com
example.org
example.net
```

Then:

```
while read domain; do
    echo "===== $domain ====="
    nslookup "$domain"
done < domains.txt
```

For only A records:

```
while read domain; do
    echo "===== $domain ====="
    nslookup -type=A "$domain"
done < domains.txt
```

---

# 40. Common Mistakes

### Mistake 1 — Putting a URL instead of a hostname

Wrong:

```
nslookup https://example.com/login
```

Correct:

```
nslookup example.com
```

For a URL such as:

```
https://www.example.com/login
```

the DNS hostname is:

```
www.example.com
```

---

### Mistake 2 — Assuming no PTR means no host

```
nslookup 203.0.113.10
```

If there is no PTR record, that doesn't mean the IP is unused.

It simply means reverse DNS doesn't provide a hostname.

---

### Mistake 3 — Assuming `NS` reveals every subdomain

```
nslookup -type=NS example.com
```

returns nameservers, **not all subdomains**.

Subdomain enumeration requires other techniques/tools.

---

# 41. Most Useful Commands to Memorize

```
# Basic lookup
nslookup example.com
```

```
# IPv4
nslookup -type=A example.com
```

```
# IPv6
nslookup -type=AAAA example.com
```

```
# Nameservers
nslookup -type=NS example.com
```

```
# Mail servers
nslookup -type=MX example.com
```

```
# TXT
nslookup -type=TXT example.com
```

```
# SOA
nslookup -type=SOA example.com
```

```
# CNAME
nslookup -type=CNAME www.example.com
```

```
# Reverse DNS
nslookup 8.8.8.8
```

```
# Specific DNS server
nslookup example.com 8.8.8.8
```

```
# Specific record + DNS server
nslookup -type=MX example.com 8.8.8.8
```

```
# SRV
nslookup -type=SRV _ldap._tcp.example.com
```

```
# CAA
nslookup -type=CAA example.com
```

---

# 42. Quick Mental Model

When you get a domain during a pentest:

```
nslookup example.com
        │
        ▼
       A/IPv4
        │
        ▼
        IP
        │
        ├── Reverse DNS
        │
        └── WHOIS
```

Then:

```
nslookup -type=NS example.com
        │
        ▼
  Authoritative DNS
```

```
nslookup -type=MX example.com
        │
        ▼
    Mail servers
```

```
nslookup -type=TXT example.com
        │
        ▼
 SPF / verification / other TXT
```

```
nslookup -type=CNAME sub.example.com
        │
        ▼
   Alias / external target
```

And for deeper DNS analysis:

```
nslookup
   ↓
quick lookup

dig
   ↓
detailed DNS analysis
```