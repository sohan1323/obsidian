
---
`host` is a simple **DNS lookup utility** commonly available on Kali/Linux systems. It is useful for quickly resolving domains, querying specific DNS record types, performing reverse DNS lookups, and querying a specific DNS server.

Compared with `dig`, `host` is intentionally simpler and produces more concise output.

---

# 1. Installation

On Kali/Debian/Ubuntu:

```
sudo apt update
sudo apt install bind9-dnsutils
```

Check:

```
host -V
```

or:

```
which host
```

Help:

```
host -h
```

Manual:

```
man host
```

---

# 2. Basic Syntax

The general syntax is:

```
host [OPTIONS] DOMAIN [DNS_SERVER]
```

Basic lookup:

```
host example.com
```

Typical result:

```
example.com has address 93.184.216.34
```

The basic lookup normally resolves the domain to its address records.

---

# 3. Understand the Basic Command

```
host example.com
```

Breakdown:

```
host
 │
 └── example.com
       │
       └── hostname/domain being queried
```

Compared with `dig`:

```
dig example.com
```

produces a detailed DNS response, while:

```
host example.com
```

gives a much cleaner result.

---

# 4. IPv4 — A Record

Explicitly request an A record:

```
host -t A example.com
```

Example output:

```
example.com has address 93.184.216.34
```

`A` means:

```
Hostname → IPv4
```

---

# 5. IPv6 — AAAA Record

```
host -t AAAA example.com
```

Example:

```
example.com has IPv6 address 2001:db8::1
```

`AAAA` means:

```
Hostname → IPv6
```

---

# 6. Nameservers — NS

Find authoritative nameservers:

```
host -t NS example.com
```

Example:

```
example.com name server ns1.example.com.
example.com name server ns2.example.com.
```

This is one of the first useful queries during DNS reconnaissance.

---

# 7. Mail Servers — MX

```
host -t MX example.com
```

Example:

```
example.com mail is handled by 10 mail.example.com.
```

The number:

```
10
```

is the MX preference.

---

# 8. TXT Records

```
host -t TXT example.com
```

Example:

```
example.com descriptive text "v=spf1 include:_spf.example.com ~all"
```

TXT records can contain:

- SPF
- Domain verification
- Service configuration
- Other arbitrary DNS information

---

# 9. SOA Record

```
host -t SOA example.com
```

The SOA record provides zone-authority information such as:

```
Primary nameserver
Responsible mailbox
Serial
Refresh
Retry
Expire
Minimum TTL
```

---

# 10. CNAME

Query a specific hostname:

```
host -t CNAME www.example.com
```

Example:

```
www.example.com is an alias for web.example.net.
```

This can be useful when determining whether a subdomain points to another hostname or external service.

---

# 11. Reverse DNS

One of the most useful `host` features.

```
host 8.8.8.8
```

Example:

```
8.8.8.8.in-addr.arpa domain name pointer dns.google.
```

You can also explicitly request PTR:

```
host -t PTR 8.8.8.8
```

Conceptually:

```
IP
 ↓
PTR
 ↓
Hostname
```

---

# 12. Reverse DNS for a Pentest IP

Suppose you discover:

```
203.0.113.10
```

Run:

```
host 203.0.113.10
```

If a PTR exists, you may get:

```
10.113.0.203.in-addr.arpa domain name pointer server.example.com.
```

You can then investigate:

```
host server.example.com
```

This creates a useful pivot:

```
IP
 ↓
PTR
 ↓
Hostname
 ↓
A
 ↓
IP
```

---

# 13. Query a Specific DNS Server

Syntax:

```
host DOMAIN DNS_SERVER
```

Example:

```
host example.com 8.8.8.8
```

This asks Google's public DNS resolver.

Cloudflare:

```
host example.com 1.1.1.1
```

This is useful for comparing DNS responses from different resolvers.

---

# 14. Specific Record + DNS Server

You can combine them:

```
host -t MX example.com 8.8.8.8
```

```
host -t NS example.com 1.1.1.1
```

```
host -t TXT example.com 8.8.8.8
```

General syntax:

```
host -t RECORD DOMAIN DNS_SERVER
```

---

# 15. `-t` — Specify Record Type

This is the most important option.

Syntax:

```
host -t TYPE DOMAIN
```

Examples:

```
host -t A example.com
```

```
host -t AAAA example.com
```

```
host -t NS example.com
```

```
host -t MX example.com
```

```
host -t TXT example.com
```

```
host -t SOA example.com
```

```
host -t CNAME www.example.com
```

---

# 16. Common Record Types

|Record|Purpose|Command|
|---|---|---|
|`A`|IPv4|`host -t A example.com`|
|`AAAA`|IPv6|`host -t AAAA example.com`|
|`NS`|Nameservers|`host -t NS example.com`|
|`MX`|Mail servers|`host -t MX example.com`|
|`TXT`|Text/configuration|`host -t TXT example.com`|
|`CNAME`|Alias|`host -t CNAME www.example.com`|
|`SOA`|Zone authority|`host -t SOA example.com`|
|`PTR`|Reverse DNS|`host -t PTR 8.8.8.8`|
|`SRV`|Service location|`host -t SRV _ldap._tcp.example.com`|
|`CAA`|Certificate authorities|`host -t CAA example.com`|
|`DS`|DNSSEC delegation|`host -t DS example.com`|
|`DNSKEY`|DNSSEC key|`host -t DNSKEY example.com`|

---

# 17. Query SRV Records

SRV records identify services.

Example:

```
host -t SRV _ldap._tcp.example.com
```

Another:

```
host -t SRV _sip._tcp.example.com
```

This can be particularly useful during authorized Active Directory/DNS reconnaissance.

For example:

```
host -t SRV _ldap._tcp.dc._msdcs.example.com
```

may reveal domain-controller-related DNS records in an Active Directory environment.

---

# 18. Query CAA

CAA records specify which certificate authorities may issue certificates for a domain.

```
host -t CAA example.com
```

Example:

```
example.com has CAA record 0 issue "letsencrypt.org"
```

Useful during certificate/DNS configuration assessment.

---

# 19. Query DNSSEC

DNSSEC records can be queried explicitly.

```
host -t DNSKEY example.com
```

```
host -t DS example.com
```

```
host -t RRSIG example.com
```

These are useful when assessing DNSSEC configuration.

---

# 20. Find All Common Records

There is an important distinction between:

```
host example.com
```

and explicitly querying record types.

For a structured DNS reconnaissance workflow, query the important types individually:

```
host -t A example.com
host -t AAAA example.com
host -t NS example.com
host -t MX example.com
host -t TXT example.com
host -t SOA example.com
```

This is generally more predictable than relying on a broad query.

---

# 21. `-a` — All Information

Depending on the version of `host`, `-a` requests a verbose/all-record style query.

```
host -a example.com
```

This is roughly useful when you want more information than the normal lookup.

However, don't interpret `-a` as a guarantee that you'll receive every DNS record. DNS servers can restrict or omit information.

For precise enumeration, explicitly query:

```
host -t A example.com
host -t MX example.com
host -t NS example.com
host -t TXT example.com
```

---

# 22. `-v` — Verbose Output

```
host -v example.com
```

This gives more information about the DNS query and response.

Useful when troubleshooting.

Compare:

```
host example.com
```

with:

```
host -v example.com
```

The second provides substantially more DNS-response detail.

---

# 23. `-W` — Timeout

You can specify a timeout.

```
host -W 5 example.com
```

Meaning:

```
-W 5
 ↓
wait up to approximately 5 seconds
```

Useful when a DNS server is slow or unreachable.

---

# 24. `-R` — Retries

Specify the number of retries:

```
host -R 3 example.com
```

This can be useful when troubleshooting unreliable DNS connectivity.

---

# 25. `-4` — IPv4 Transport

Force IPv4:

```
host -4 example.com
```

Useful when troubleshooting IPv4/IPv6 connectivity.

---

# 26. `-6` — IPv6 Transport

Force IPv6:

```
host -6 example.com
```

---

# 27. Zone Transfer — AXFR

`host` can be used to request a DNS zone transfer.

Syntax:

```
host -l example.com ns1.example.com
```

Where:

```
-l
 ↓
list/attempt zone transfer

example.com
 ↓
zone

ns1.example.com
 ↓
DNS server
```

For an authorized test:

```
host -l example.com ns1.example.com
```

If AXFR is allowed, the server may return multiple DNS records.

A properly configured public DNS server will generally refuse unauthorized zone transfers.

For detailed AXFR testing, `dig` is usually easier:

```
dig @ns1.example.com example.com AXFR
```

Only perform this against systems you are authorized to test.

---

# 28. Find Authoritative Servers Before AXFR

First:

```
host -t NS example.com
```

Suppose:

```
example.com name server ns1.example.com.
example.com name server ns2.example.com.
```

Then an authorized assessment can test:

```
host -l example.com ns1.example.com
```

and:

```
host -l example.com ns2.example.com
```

Conceptually:

```
Domain
  ↓
NS records
  ↓
Authoritative DNS servers
  ↓
AXFR test
```

---

# 29. DNS Reconnaissance Workflow

For an authorized target:

### Step 1 — A

```
host example.com
```

### Step 2 — IPv6

```
host -t AAAA example.com
```

### Step 3 — Nameservers

```
host -t NS example.com
```

### Step 4 — Mail

```
host -t MX example.com
```

### Step 5 — TXT

```
host -t TXT example.com
```

### Step 6 — SOA

```
host -t SOA example.com
```

### Step 7 — Reverse DNS

```
host <IP>
```

### Step 8 — CNAME for interesting subdomains

```
host -t CNAME dev.example.com
```

---

# 30. `host` + `whois`

Suppose:

```
host example.com
```

returns:

```
example.com has address 203.0.113.10
```

Then:

```
whois 203.0.113.10
```

This lets you pivot from:

```
Domain
 ↓
IP
 ↓
Network ownership
```

Then:

```
host 203.0.113.10
```

for reverse DNS.

---

# 31. `host` + `dig`

These tools complement each other.

### Quick lookup

```
host example.com
```

### Detailed lookup

```
dig example.com
```

### Quick NS lookup

```
host -t NS example.com
```

### Detailed NS lookup

```
dig example.com NS
```

### Quick reverse lookup

```
host 8.8.8.8
```

### Detailed reverse lookup

```
dig -x 8.8.8.8
```

### DNS delegation

```
dig example.com +trace
```

`dig` is generally the better tool when you need to inspect the full DNS protocol response.

---

# 32. Subdomain Reconnaissance

Suppose you already have a list:

```
www
mail
vpn
dev
test
api
```

You can resolve them individually:

```
host www.example.com
host mail.example.com
host vpn.example.com
host dev.example.com
host test.example.com
host api.example.com
```

Or automate:

```
while read sub; do
    host "$sub.example.com"
done < subdomains.txt
```

Better formatted:

```
while read sub; do
    echo "===== $sub.example.com ====="
    host "$sub.example.com"
done < subdomains.txt
```

---

# 33. Extract Only Resolved Addresses

You can combine `host` with standard Linux tools.

For example:

```
host example.com | grep "has address"
```

For IPv6:

```
host -t AAAA example.com | grep "IPv6 address"
```

This is useful when feeding results into another script/tool.

---

# 34. Multiple Domains

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
    host "$domain"
done < domains.txt
```

Only A records:

```
while read domain; do
    echo "===== $domain ====="
    host -t A "$domain"
done < domains.txt
```

---

# 35. Save Results

Save one lookup:

```
host example.com > dns.txt
```

Append another:

```
host -t MX example.com >> dns.txt
```

Multiple queries:

```
{
    host example.com
    host -t NS example.com
    host -t MX example.com
    host -t TXT example.com
} > dns-recon.txt
```

---

# 36. Simple DNS Recon Script

For an authorized assessment:

```
#!/bin/bash

domain="$1"

echo "===== A ====="
host -t A "$domain"

echo
echo "===== AAAA ====="
host -t AAAA "$domain"

echo
echo "===== NS ====="
host -t NS "$domain"

echo
echo "===== MX ====="
host -t MX "$domain"

echo
echo "===== TXT ====="
host -t TXT "$domain"

echo
echo "===== SOA ====="
host -t SOA "$domain"
```

Save as:

```
dns-recon.sh
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

# 37. Important Error Messages

### `NXDOMAIN`

Example:

```
Host nonexistent.example.com not found: 3(NXDOMAIN)
```

Means the DNS system indicates that the queried name doesn't exist.

---

### `SERVFAIL`

Indicates the DNS server failed to successfully process the query.

Possible causes include DNS-server problems, DNSSEC validation issues, or upstream failures.

---

### `REFUSED`

The DNS server refused the query.

This may happen because of access-control or server policy.

---

### Timeout

If the DNS server doesn't respond within the configured timeout, you may see a timeout-related error.

You can increase the timeout:

```
host -W 10 example.com
```

---

# 38. Common Mistakes

### Mistake 1 — Using a URL

Wrong:

```
host https://example.com/login
```

Correct:

```
host example.com
```

For:

```
https://www.example.com/login
```

the hostname is:

```
www.example.com
```

---

### Mistake 2 — Assuming `host example.com` finds subdomains

It doesn't.

```
host example.com
```

primarily resolves the specified hostname.

It does **not** enumerate:

```
admin.example.com
dev.example.com
vpn.example.com
api.example.com
```

You need a subdomain enumeration method/tool for that.

---

### Mistake 3 — Assuming no PTR means the IP is invalid

```
host 203.0.113.10
```

If no hostname is returned, that simply means there may be no useful reverse-DNS record.

---

# 39. Most Important Options

|Option|Purpose|Example|
|---|---|---|
|`-t`|Record type|`host -t MX example.com`|
|`-a`|All/verbose query|`host -a example.com`|
|`-v`|Verbose|`host -v example.com`|
|`-W`|Timeout|`host -W 5 example.com`|
|`-R`|Retries|`host -R 3 example.com`|
|`-4`|IPv4 transport|`host -4 example.com`|
|`-6`|IPv6 transport|`host -6 example.com`|
|`-l`|Zone listing/AXFR|`host -l example.com ns1.example.com`|

---

# 40. Commands You Should Memorize

### Basic

```
host example.com
```

### IPv4

```
host -t A example.com
```

### IPv6

```
host -t AAAA example.com
```

### Nameservers

```
host -t NS example.com
```

### Mail

```
host -t MX example.com
```

### TXT

```
host -t TXT example.com
```

### SOA

```
host -t SOA example.com
```

### CNAME

```
host -t CNAME www.example.com
```

### Reverse DNS

```
host 8.8.8.8
```

### Specific DNS server

```
host example.com 8.8.8.8
```

### SRV

```
host -t SRV _ldap._tcp.example.com
```

### CAA

```
host -t CAA example.com
```

### DNSSEC

```
host -t DNSKEY example.com
```

### Authorized AXFR test

```
host -l example.com ns1.example.com
```

---

# 41. `host` vs `nslookup` vs `dig`

Since you're learning these tools sequentially, keep this mental model:

```
                 DNS QUERY
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
       host      nslookup       dig
        │           │            │
        ▼           ▼            ▼
      Simple      Simple       Detailed
      output      queries      analysis
```

|Task|`host`|`nslookup`|`dig`|
|---|---|---|---|
|Quick A lookup|⭐⭐⭐|⭐⭐⭐|⭐⭐⭐|
|Quick MX/NS/TXT|⭐⭐⭐|⭐⭐⭐|⭐⭐⭐|
|Reverse DNS|⭐⭐⭐|⭐⭐⭐|⭐⭐⭐|
|Specific DNS server|⭐⭐⭐|⭐⭐⭐|⭐⭐⭐|
|Interactive querying|❌|⭐⭐⭐|⭐⭐⭐|
|Detailed response analysis|⭐|⭐⭐|⭐⭐⭐|
|DNS tracing|❌|Limited|⭐⭐⭐|
|Scripting|⭐⭐⭐|⭐⭐|⭐⭐⭐|
|AXFR|⭐⭐|⭐⭐|⭐⭐⭐|

### Practical rule

**`host` → quick DNS lookup**

```
host example.com
```

**`nslookup` → simple interactive DNS investigation**

```
nslookup
```

**`dig` → detailed/professional DNS analysis**

```
dig example.com
```