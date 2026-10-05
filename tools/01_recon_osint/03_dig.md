
---
`dig` (**Domain Information Groper**) is a command-line DNS query tool from the BIND suite. It lets you directly query DNS servers and inspect DNS records, response codes, TTLs, flags, authoritative servers, and other DNS information. It is one of the most useful tools for **DNS reconnaissance and troubleshooting**. [BIND 9 Documentation](https://bind9.readthedocs.io/en/v9.21.7/manpages.html?utm_source=chatgpt.com)

For pentesting, use it primarily for **authorized targets**.

---

# 1. Installation

On Kali:

```
sudo apt update
sudo apt install bind9-dnsutils
```

Check:

```
dig -v
```

Help:

```
dig -h
```

Manual:

```
man dig
```

---

# 2. Basic Syntax

The basic structure is:

```
dig [@DNS_SERVER] DOMAIN [RECORD_TYPE] [OPTIONS]
```

For example:

```
dig example.com
```

Equivalent explicit form:

```
dig example.com A
```

The default query type is `A` when no type is specified. [BIND 9 Documentation](https://bind9.readthedocs.io/en/v9.21.7/manpages.html?utm_source=chatgpt.com)

---

# 3. Understand the Command Structure

Take:

```
dig @8.8.8.8 example.com MX +short
```

Breakdown:

```
dig
│
├── @8.8.8.8
│      └── DNS server to query
│
├── example.com
│      └── domain
│
├── MX
│      └── DNS record type
│
└── +short
       └── simplified output
```

The general professional pattern is:

```
dig @SERVER DOMAIN TYPE OPTIONS
```

---

# 4. Basic A Record Lookup

```
dig example.com A
```

An `A` record maps a hostname to an IPv4 address.

Typical result:

```
;; ANSWER SECTION:
example.com.    300    IN    A    93.184.216.34
```

The important part is:

```
example.com → 93.184.216.34
```

---

# 5. Simplify Output with `+short`

Instead of the complete DNS response:

```
dig example.com A +short
```

Output:

```
93.184.216.34
```

This is extremely useful for scripts and reconnaissance.

For example:

```
ip=$(dig example.com A +short)
echo "$ip"
```

---

# 6. Query AAAA Records

`AAAA` records provide IPv6 addresses.

```
dig example.com AAAA
```

Short form:

```
dig example.com AAAA +short
```

Example:

```
2001:db8::1
```

---

# 7. Query MX Records

`MX` records identify mail servers.

```
dig example.com MX
```

Short:

```
dig example.com MX +short
```

Example:

```
10 mail.example.com.
20 mail2.example.com.
```

The number is the **mail exchanger preference**.

Lower preference value generally has priority.

---

# 8. Query NS Records

`NS` records identify authoritative nameservers.

```
dig example.com NS
```

Short:

```
dig example.com NS +short
```

Example:

```
ns1.example.com.
ns2.example.com.
```

This is one of the first queries you should perform during DNS reconnaissance.

---

# 9. Query TXT Records

TXT records can contain many types of information.

```
dig example.com TXT
```

Short:

```
dig example.com TXT +short
```

TXT records commonly contain things such as:

- SPF information
- Domain verification data
- Service configuration
- Other arbitrary DNS text

For example:

```
"v=spf1 include:_spf.example.com ~all"
```

---

# 10. Query SOA

`SOA` = **Start of Authority**.

```
dig example.com SOA
```

Example:

```
example.com.  3600  IN  SOA  ns1.example.com. admin.example.com. ...
```

The SOA record can provide information such as:

```
Primary nameserver
Administrative mailbox
Serial number
Refresh
Retry
Expire
Minimum/negative-cache TTL
```

This is useful for understanding the DNS zone's authoritative configuration.

---

# 11. Query CNAME

`CNAME` identifies an alias.

```
dig www.example.com CNAME
```

Short:

```
dig www.example.com CNAME +short
```

Example:

```
web.example.net.
```

This can be useful during reconnaissance because a subdomain may point to an external service.

---

# 12. Query PTR

A `PTR` record is used for reverse DNS.

You can query it directly:

```
dig -x 8.8.8.8
```

Or:

```
dig -x 8.8.8.8 +short
```

Example:

```
dns.google.
```

`-x` automatically constructs the reverse-DNS query and performs a PTR lookup. [Linux Die](https://linux.die.net/man/1/dig?utm_source=chatgpt.com)

---

# 13. Reverse DNS on a Target IP

Suppose reconnaissance gives:

```
203.0.113.10
```

Run:

```
dig -x 203.0.113.10
```

Short:

```
dig -x 203.0.113.10 +short
```

Conceptually:

```
IP address
    ↓
PTR query
    ↓
Hostname
```

Reverse DNS isn't guaranteed to exist.

---

# 14. Query a Specific DNS Server

Normally `dig` uses the resolver configured on your system, commonly through `/etc/resolv.conf`. You can explicitly select a DNS server using `@server`. [BIND 9 Documentation](https://bind9.readthedocs.io/en/v9.21.7/manpages.html?utm_source=chatgpt.com)

Google DNS:

```
dig @8.8.8.8 example.com
```

Cloudflare DNS:

```
dig @1.1.1.1 example.com
```

Query a specific record:

```
dig @8.8.8.8 example.com MX
```

Short:

```
dig @8.8.8.8 example.com MX +short
```

---

# 15. Query the Authoritative Nameserver Directly

Suppose:

```
dig example.com NS +short
```

returns:

```
ns1.example.com.
ns2.example.com.
```

You can query one directly:

```
dig @ns1.example.com example.com A
```

This is useful because you're now asking the authoritative server directly instead of your normal recursive resolver.

---

# 16. Find the DNS Server Used

Run:

```
dig example.com
```

Look at:

```
;; SERVER: ...
```

For example:

```
;; SERVER: 192.168.1.1#53
```

This tells you which resolver supplied the response.

---

# 17. Understand the Output

A normal `dig` response contains several sections.

Example structure:

```
; <<>> DiG <<>> example.com A
;; global options: +cmd

;; QUESTION SECTION:
;example.com.        IN      A

;; ANSWER SECTION:
example.com.  300    IN      A    93.184.216.34

;; AUTHORITY SECTION:
...

;; ADDITIONAL SECTION:
...

;; Query time: 20 msec
;; SERVER: 192.168.1.1#53
;; WHEN: ...
;; MSG SIZE  rcvd: ...
```

---

# 18. QUESTION SECTION

Example:

```
;; QUESTION SECTION:
;example.com.        IN      A
```

Means:

```
Name:
example.com

Class:
IN = Internet

Type:
A
```

---

# 19. ANSWER SECTION

Example:

```
example.com.  300  IN  A  93.184.216.34
```

Breakdown:

```
example.com
     ↓
Name

300
     ↓
TTL

IN
     ↓
Internet class

A
     ↓
Record type

93.184.216.34
     ↓
Answer
```

---

# 20. TTL

TTL = **Time To Live**.

Example:

```
example.com. 300 IN A 93.184.216.34
```

`300` is the TTL in seconds.

It indicates how long a resolver may cache the record before needing to refresh it.

---

# 21. AUTHORITY SECTION

The authority section can contain information about authoritative DNS servers.

Example:

```
;; AUTHORITY SECTION:
example.com. 86400 IN NS ns1.example.com.
```

This is especially useful when the queried record isn't directly available in the answer section.

---

# 22. ADDITIONAL SECTION

This may contain related records supplied by the DNS server.

For example:

```
;; ADDITIONAL SECTION:
ns1.example.com. 86400 IN A 203.0.113.53
```

It can save you from making another DNS query.

---

# 23. Query Status

Look at:

```
;; ->>HEADER<<- opcode: QUERY, status: NOERROR
```

Common statuses:

|Status|Meaning|
|---|---|
|`NOERROR`|Query succeeded|
|`NXDOMAIN`|Domain/name doesn't exist|
|`SERVFAIL`|Server failed to complete query|
|`REFUSED`|Server refused the query|
|`FORMERR`|Query format error|

---

# 24. `+short`

One of the most useful options.

```
dig example.com +short
```

A:

```
dig example.com A +short
```

MX:

```
dig example.com MX +short
```

NS:

```
dig example.com NS +short
```

TXT:

```
dig example.com TXT +short
```

CNAME:

```
dig www.example.com CNAME +short
```

Use it when you only care about the answer rather than the full DNS response.

---

# 25. `+noall +answer`

Another excellent output format:

```
dig example.com +noall +answer
```

Example:

```
example.com. 300 IN A 93.184.216.34
```

This is often better for scripts because it displays the answer section while removing most other output.

---

# 26. `+stats`

Display query statistics:

```
dig example.com +stats
```

Useful information includes:

```
Query time
Server
When
Message size
```

---

# 27. `+trace`

One of the most important advanced options.

```
dig example.com +trace
```

Instead of simply asking your normal resolver for the answer, `dig` follows the DNS delegation path.

Conceptually:

```
Root DNS
   ↓
.com nameserver
   ↓
example.com authoritative server
   ↓
Answer
```

This is useful for understanding **how DNS delegation works** and troubleshooting DNS resolution.

---

# 28. `+trace` with a Specific Record

```
dig example.com MX +trace
```

or:

```
dig example.com NS +trace
```

This allows you to observe the delegation process for that query.

---

# 29. DNSSEC Information

Request DNSSEC-related records:

```
dig example.com DNSKEY
```

You can also request:

```
dig example.com DS
```

And:

```
dig example.com RRSIG
```

Useful for DNSSEC assessment.

---

# 30. `+dnssec`

Request DNSSEC-related data where applicable:

```
dig example.com +dnssec
```

This can cause DNSSEC records such as `RRSIG` to be included in responses when available.

---

# 31. Query `ANY`

You may see:

```
dig example.com ANY
```

Historically, this was used to request multiple record types.

However, **don't rely on `ANY` as a "give me everything" command**. Modern DNS infrastructure may refuse, minimize, or otherwise handle ANY queries differently.

Instead, explicitly query:

```
dig example.com A
dig example.com AAAA
dig example.com MX
dig example.com NS
dig example.com TXT
dig example.com SOA
```

This is more reliable.

---

# 32. Zone Transfer — `AXFR`

A DNS zone transfer can be requested using:

```
dig @ns1.example.com example.com AXFR
```

Syntax:

```
dig @NAMESERVER DOMAIN AXFR
```

Example:

```
dig @ns1.example.com example.com AXFR
```

### Important

A properly configured public authoritative DNS server will normally **not** allow arbitrary zone transfers.

If an authorized test environment permits AXFR, the response can contain many DNS records.

Conceptually:

```
AXFR
 ↓
Entire DNS zone
 ↓
Hosts
Mail servers
Subdomains
DNS records
etc.
```

Only test this against infrastructure you are authorized to assess.

---

# 33. Check Multiple Nameservers for AXFR

If:

```
dig example.com NS +short
```

returns:

```
ns1.example.com.
ns2.example.com.
```

An authorized assessment could test each authoritative server:

```
dig @ns1.example.com example.com AXFR
```

```
dig @ns2.example.com example.com AXFR
```

If refused:

```
Transfer failed.
```

that is expected for many properly configured servers.

---

# 34. `-t` — Specify Record Type

Instead of:

```
dig example.com MX
```

you can use:

```
dig -t MX example.com
```

Likewise:

```
dig -t A example.com
```

```
dig -t NS example.com
```

```
dig -t TXT example.com
```

The `-t` option explicitly sets the DNS record type. [Debian Manpages](https://manpages.debian.org/bookworm/bind9-dnsutils/dig.1.en.html?utm_source=chatgpt.com)

---

# 35. `-q` — Specify Query Name

```
dig -q example.com A
```

This explicitly tells `dig` the name being queried.

It is particularly useful in complex commands where you want to clearly distinguish the query name from other arguments. [Debian Manpages](https://manpages.debian.org/bookworm/bind9-dnsutils/dig.1.en.html?utm_source=chatgpt.com)

---

# 36. `-4` — IPv4 Only

```
dig -4 example.com
```

This forces IPv4 transport.

Useful when troubleshooting systems where IPv6 connectivity is causing problems.

---

# 37. `-6` — IPv6 Only

```
dig -6 example.com
```

Forces IPv6 transport.

---

# 38. `-p` — Custom DNS Port

DNS normally uses port:

```
53
```

You can specify another port:

```
dig -p 5353 example.com
```

Combined with a server:

```
dig @192.0.2.10 -p 5353 example.com
```

The `-p` option is useful when testing a DNS server configured to listen on a non-standard port. [Debian Manpages](https://manpages.debian.org/bookworm/bind9-dnsutils/dig.1.en.html?utm_source=chatgpt.com)

---

# 39. `-f` — Batch Mode

Suppose you have:

```
domains.txt
```

containing:

```
example.com
example.org
example.net
```

You can process queries from a file:

```
dig -f domains.txt
```

BIND's `dig` supports batch mode through `-f`. [BIND 9 Documentation](https://bind9.readthedocs.io/en/v9.21.7/manpages.html?utm_source=chatgpt.com)

For specific record types, prepare queries appropriately or use a shell loop.

---

# 40. Query Many Domains with Bash

For pentesting reconnaissance:

```
while read domain; do
    echo "===== $domain ====="
    dig "$domain" A +short
done < domains.txt
```

Output might look like:

```
===== example.com =====
93.184.216.34

===== example.org =====
192.0.43.8
```

---

# 41. Enumerate Common DNS Records

For one authorized domain:

```
domain="example.com"

dig "$domain" A +short
dig "$domain" AAAA +short
dig "$domain" MX +short
dig "$domain" NS +short
dig "$domain" TXT +short
dig "$domain" SOA +short
```

This gives you a quick DNS profile.

---

# 42. Subdomain DNS Reconnaissance

Suppose you have:

```
www.example.com
mail.example.com
vpn.example.com
dev.example.com
```

Query them:

```
dig www.example.com A +short
```

```
dig mail.example.com A +short
```

```
dig vpn.example.com A +short
```

```
dig dev.example.com A +short
```

You can automate this:

```
while read subdomain; do
    echo "===== $subdomain ====="
    dig "$subdomain.example.com" A +short
done < subdomains.txt
```

---

# 43. Check for CNAMEs

This is particularly useful for understanding where a subdomain points.

```
dig dev.example.com CNAME +short
```

Example:

```
some-service.example.net.
```

Then investigate the resulting hostname:

```
dig some-service.example.net A +short
```

During authorized testing, CNAME relationships can also help identify externally hosted services and potential dangling-resource issues, but the DNS result alone does **not** prove a takeover vulnerability.

---

# 44. SPF Reconnaissance

Query TXT:

```
dig example.com TXT +short
```

Look for:

```
v=spf1
```

Example:

```
"v=spf1 include:_spf.example.com -all"
```

This can tell you which services are authorized to send mail for the domain.

---

# 45. DMARC Reconnaissance

DMARC normally exists at:

```
_dmarc.example.com
```

Query:

```
dig _dmarc.example.com TXT +short
```

Example:

```
"v=DMARC1; p=reject; ..."
```

This is useful during email-security assessment.

---

# 46. DKIM Reconnaissance

DKIM records use a selector.

For example, if the selector is:

```
google
```

query:

```
dig google._domainkey.example.com TXT +short
```

The selector must be known or discovered through authorized testing/documentation.

---

# 47. DNS Recon Workflow

A useful workflow is:

```
                DOMAIN
                   │
                   ▼
              dig A
                   │
                   ▼
                  IP
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
      dig AAAA             Reverse DNS
                              │
                              ▼
                           hostname
```

Then:

```
DOMAIN
  │
  ├── NS
  ├── MX
  ├── TXT
  ├── SOA
  └── CNAME
```

Then investigate relevant hosts individually.

---

# 48. Dig + WHOIS Workflow

Since you learned WHOIS first, combine them.

### Step 1 — WHOIS

```
whois example.com
```

### Step 2 — Nameservers

```
dig example.com NS +short
```

### Step 3 — IP

```
dig example.com A +short
```

### Step 4 — IP WHOIS

```
whois <IP>
```

### Step 5 — Reverse DNS

```
dig -x <IP> +short
```

### Step 6 — Mail infrastructure

```
dig example.com MX +short
```

### Step 7 — TXT

```
dig example.com TXT +short
```

This gives you a basic passive DNS profile.

---

# 49. Important `dig` Options

|Option|Meaning|Example|
|---|---|---|
|`@server`|Query specific DNS server|`dig @8.8.8.8 example.com`|
|`-x`|Reverse DNS|`dig -x 8.8.8.8`|
|`-t`|Specify record type|`dig -t MX example.com`|
|`-q`|Specify query name|`dig -q example.com A`|
|`-f`|Batch file|`dig -f queries.txt`|
|`-p`|DNS port|`dig -p 5353 example.com`|
|`-4`|IPv4 transport|`dig -4 example.com`|
|`-6`|IPv6 transport|`dig -6 example.com`|
|`-h`|Help|`dig -h`|
|`+short`|Short output|`dig example.com +short`|
|`+trace`|Trace DNS delegation|`dig example.com +trace`|
|`+dnssec`|Request DNSSEC data|`dig example.com +dnssec`|
|`+stats`|Show statistics|`dig example.com +stats`|
|`+noall`|Suppress sections|`dig example.com +noall`|
|`+answer`|Show answer section|`dig example.com +answer`|

The available options can vary somewhat with the installed BIND version, so `dig -h` and the local manual are the authoritative references for your installation. [BIND 9 Documentation](https://bind9.readthedocs.io/en/v9.21.7/manpages.html?utm_source=chatgpt.com)

---

# 50. Most Important Record Types

Memorize these:

|Record|Purpose|
|---|---|
|`A`|Hostname → IPv4|
|`AAAA`|Hostname → IPv6|
|`CNAME`|Alias → canonical hostname|
|`MX`|Mail servers|
|`NS`|Nameservers|
|`TXT`|Text/configuration information|
|`SOA`|Zone authority information|
|`PTR`|IP → hostname|
|`SRV`|Service location|
|`CAA`|Certificate-authority authorization|
|`DS`|DNSSEC delegation|
|`DNSKEY`|DNSSEC public keys|
|`RRSIG`|DNSSEC signatures|
|`AXFR`|Full zone transfer request|
|`IXFR`|Incremental zone transfer|

---

# 51. Very Useful Commands to Memorize

### Basic

```
dig example.com
```

### IPv4

```
dig example.com A +short
```

### IPv6

```
dig example.com AAAA +short
```

### Nameservers

```
dig example.com NS +short
```

### Mail

```
dig example.com MX +short
```

### TXT

```
dig example.com TXT +short
```

### SOA

```
dig example.com SOA +short
```

### Reverse lookup

```
dig -x 8.8.8.8 +short
```

### Specific DNS server

```
dig @8.8.8.8 example.com
```

### DNS delegation trace

```
dig example.com +trace
```

### DNSSEC

```
dig example.com DNSKEY
```

### Authorized AXFR test

```
dig @ns1.example.com example.com AXFR
```

### Clean answer

```
dig example.com +noall +answer
```

---

# 52. Professional Mental Model

When you receive a domain during a pentest, think:

```
                 example.com
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
      A/AAAA          NS             MX
       │              │              │
       ▼              ▼              ▼
      IPs         DNS servers      Mail servers
       │
       ▼
   Reverse DNS
       │
       ▼
   Hostnames
```

Then:

```
A / AAAA
   ↓
Identify IPs
   ↓
WHOIS / network ownership
   ↓
Reverse DNS
   ↓
Additional DNS records
   ↓
Authorized service enumeration
```