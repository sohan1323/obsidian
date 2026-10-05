
---
**DNS (Domain Name System)** is the system that translates **human-readable domain names into IP addresses** so computers can locate servers on a network.

Browser
   │
   ↓
DNS Resolver
   │
   ↓
Root DNS Server
   │
   ↓
TLD DNS Server (.com)
   │
   ↓
Authoritative DNS Server
   │
   ↓
IP address
   │
   ↓
Browser connects to server


# Domain Name

A **domain name** is a human-readable name used to identify a website or other Internet resource instead of requiring users to remember an IP address.

For example:

```
google.com
github.com
example.com
```

www      . example . com
│            │                   │
│            │                   └── TLD
│            └──────────── Domain name
└───────────────────────── Subdomain/host

**TLD = Top-Level Domain**

Examples:

```
.com
.org
.net
.edu
.gov
.in
.uk
```

### Second-Level Domain

In:

```
example.com
```

`example` is the domain registered under `.com`.

So:

```
example.com
└──────┬─────┘
       │
    Domain
```

### `www` — Subdomain

In:

```
www.example.com
```

`www` is a hostname/subdomain under `example.com`.

Other examples:

```
mail.example.com
api.example.com
admin.example.com
dev.example.com
```
# Domain Name vs URL

These are **not the same thing**.

### Domain name

```
example.com
```

### URL

```
https://www.example.com/login?user=123
```

A URL can contain much more information:

```
https://www.example.com/login?user=123
│       │               │      │
│       │               │      └── Query parameter
│       │               └───────── Path
│       └───────────────────────── Domain/host
└───────────────────────────────── Protocol
```

# TLD — Top-Level Domain

A **TLD (Top-Level Domain)** is the **last part of a domain name**, appearing after the final dot (`.`).

For example:

```
www.example.com
             ↑
            TLD
```

Here:

- `www` → subdomain/hostname
- `example` → second-level domain
- `.com` → **TLD**

---

## 1. Common TLDs

|TLD|Meaning / Common Use|
|---|---|
|`.com`|Commercial / general use|
|`.org`|Organizations|
|`.net`|Originally network-related|
|`.edu`|Educational institutions|
|`.gov`|Government|
|`.mil`|Military|
|`.int`|Certain international organizations|

Modern usage isn't always restricted according to the original meanings; for example, `.com` is broadly used.

# ccTLD — Country Code TLD

These are generally **two-letter TLDs associated with countries or territories**.

|TLD|Country/Territory|
|---|---|
|`.in`|India|
|`.uk`|United Kingdom|
|`.us`|United States|
|`.de`|Germany|
|`.fr`|France|
|`.jp`|Japan|
|`.au`|Australia|
|`.ca`|Canada|
|`.cn`|China|

Example:

```
example.in
       ↑
      ccTLD
```

# gTLD — Generic TLD

**gTLD = Generic Top-Level Domain**

Examples:

```
.com
.org
.net
.info
.biz
```

There are also many newer gTLDs:

```
.dev
.app
.tech
.shop
.cloud
.online
```

For example:

```
example.dev
example.shop
example.tech
```

# TLD Hierarchy

Consider:

```
www.example.co.in
```

Break it down:

```
www . example . co . in
 │       │       │    │
 │       │       │    └── ccTLD
 │       │       └─────── second-level domain under .in
 │       └────────────── registered domain
 └────────────────────── hostname/subdomain
```

In this case:

```
.in
```

is the **TLD**, while:

```
.co.in
```

is a **multi-label domain suffix commonly used for commercial entities in India**.

# Subdomain

A **subdomain** is a domain that exists **under a primary domain** and is commonly used to separate different websites, applications, or services belonging to the same organization.

For example:

```
example.com
```

could have:

```
www.example.com
api.example.com
mail.example.com
admin.example.com
dev.example.com
```

Here, `api`, `mail`, `admin`, and `dev` are **subdomain labels**.

---

## 1. Basic Structure

Consider:

```
api.example.com
```

Break it down:

```
api      . example . com
│              │       │
│              │       └── TLD
│              └────────── Registered domain
└───────────────────────── Subdomain
```

## Common Subdomains

Organizations commonly use subdomains for different purposes:

|Subdomain|Typical Purpose|
|---|---|
|`www.example.com`|Main website|
|`api.example.com`|API|
|`admin.example.com`|Administration panel|
|`mail.example.com`|Mail service|
|`dev.example.com`|Development environment|
|`test.example.com`|Testing environment|
|`staging.example.com`|Staging environment|
|`app.example.com`|Web application|
|`blog.example.com`|Blog|
|`shop.example.com`|E-commerce|
|`vpn.example.com`|VPN portal|
|`cdn.example.com`|CDN/content delivery|

These are conventions, not guarantees—the actual purpose depends on the organization's configuration.

# Subdomain Hierarchy

A domain can have **multiple levels** of subdomains.

For example:

```
dev.api.example.com
```

can be visualized as:

```
example.com
    │
    └── api.example.com
             │
             └── dev.api.example.com
```

Another example:

```
login.auth.example.com
```

```
example.com
    │
    └── auth.example.com
             │
             └── login.auth.example.com
```

There can technically be multiple labels to the left of the registered domain.

# FQDN — Fully Qualified Domain Name

A **Fully Qualified Domain Name (FQDN)** is the **complete domain name that identifies a specific host or service in the DNS hierarchy**.

In simple terms:

> **FQDN = complete hostname + complete domain hierarchy**

### Example

```
www.example.com
```

This is an FQDN because it specifies the complete name of the host.

---

## 1. Breaking down an FQDN

Consider:

```
www.example.com
```

```
www       . example . com
│             │        │
│             │        └── TLD
│             └─────────── Domain
└───────────────────────── Hostname / subdomain
```

So:

```
www.example.com
```

is the **fully qualified name**.

---

## 2. FQDN vs Domain Name

This distinction is important.

### Domain

```
example.com
```

This identifies the domain/namespace.

### FQDN

```
www.example.com
api.example.com
mail.example.com
```

These identify specific hosts/services within that namespace.

For example:

```
example.com
   │
   ├── www.example.com
   ├── api.example.com
   ├── mail.example.com
   └── admin.example.com
```

---

## 3. FQDN can have multiple subdomain levels

For example:

```
dev.api.example.com
```

This can be an FQDN:

```
dev
 │
 └── api
      │
      └── example
            │
            └── com
```

Another example:

```
login.auth.company.example.com
```

The important idea is that **all DNS labels needed to identify the host are present**.

---

# 4. FQDN and the trailing dot

Technically, the DNS hierarchy has a root represented by `.`.

So the absolute FQDN can be written as:

```
www.example.com.
```

The final dot means:

```
www → example → com → root
```

Compare:

```
www.example.com
```

and:

```
www.example.com.
```

The second explicitly shows the DNS root.

In everyday web usage, the trailing dot is usually omitted.


# DNS Resolution Example

Suppose you request:

```
www.example.com
```

### Step 1 — Your computer asks a recursive resolver

```
Computer
    │
    │ www.example.com ?
    ▼
Recursive DNS Resolver
```

If the resolver doesn't already have the answer cached, it starts querying DNS infrastructure.

### Step 2 — Resolver asks the root

```
Resolver
    │
    │ "Who handles .com?"
    ▼
Root Server
```

Root responds essentially:

```
"I don't know www.example.com,
but here are the name servers for .com."
```

### Step 3 — Resolver asks the `.com` TLD server

```
Resolver
    │
    │ "Who handles example.com?"
    ▼
.com TLD Server
```

The TLD server responds with the authoritative name servers for:

```
example.com
```

### Step 4 — Resolver asks the authoritative server

```
Resolver
    │
    │ "What is www.example.com?"
    ▼
Authoritative DNS
```

It might respond:

```
www.example.com → 93.184.216.34
```

The resolver returns that answer to your computer.

# "13 Root Servers" — What Does That Mean?

You will often hear:

> "There are 13 DNS root servers."

This is slightly misleading.

There are **13 root server identities**, named:

```
A-root
B-root
C-root
D-root
E-root
F-root
G-root
H-root
I-root
J-root
K-root
L-root
M-root
```

But there are **many physical/anycast instances** of these servers distributed around the world.

So:

```
13 logical identities
        ↓
Many physical locations
        ↓
Global DNS infrastructure
```

This allows root DNS to handle enormous numbers of queries while providing redundancy and low latency.

| Term            | Meaning                                            |
| --------------- | -------------------------------------------------- |
| **Root zone**   | The DNS database containing information about TLDs |
| **Root server** | Server infrastructure that serves the root zone    |
| **Root DNS**    | Informal term for the root-level DNS system        |
# TLD Servers

**TLD servers (Top-Level Domain servers)** are the second major level in the DNS hierarchy, directly below the **root servers**.

Their main job is to tell DNS resolvers **which authoritative name servers are responsible for a particular domain**.

### DNS hierarchy

```
                    Root
                     .
                     │
             ┌───────┼────────┐
            .com     .org     .in
             │
          TLD Server
             │
        example.com
             │
     Authoritative DNS
             │
      www.example.com
```

# Authoritative DNS Servers

An **authoritative DNS server** is the DNS server that contains the **official DNS records for a domain or DNS zone**.

In simple terms:

> **The authoritative server is the final source of truth for a domain's DNS records.**

# What does an authoritative server do?

Suppose `example.com` has these records:

```
example.com          A       93.184.216.34
www.example.com      A       93.184.216.34
api.example.com      A       203.0.113.10
mail.example.com     A       203.0.113.20
example.com          MX      mail.example.com
```

These records are maintained in the DNS zone managed by the domain's authoritative DNS infrastructure.

When a resolver asks:

```
"What is the IP address of api.example.com?"
```

the authoritative server can answer:

```
api.example.com → 203.0.113.10
```

|                            | Recursive Resolver   | Authoritative Server                |
| -------------------------- | -------------------- | ----------------------------------- |
| Main purpose               | Find answers         | Provide authoritative answers       |
| Searches other DNS servers | Yes                  | Normally no                         |
| Caches answers             | Usually              | Not its primary role                |
| Owns DNS zone data         | No                   | Yes                                 |
| Example role               | `1.1.1.1`, `8.8.8.8` | DNS servers hosting a domain's zone |
# Zone

A **DNS zone** is the portion of the DNS namespace managed by a particular administrative authority.

For example:

```
example.com
├── example.com
├── www.example.com
├── api.example.com
├── mail.example.com
└── dev.example.com
```

The authoritative DNS server serves the records in that zone.

This is why you'll often hear:

> "The authoritative server for the `example.com` zone."

# Recursive DNS Resolver

A **recursive DNS resolver** is a DNS server that receives a DNS query from a client and **finds the final answer on the client's behalf**.

In simple terms:

> **The recursive resolver does the DNS lookup work for you.**

Common public recursive resolvers include:

- Google Public DNS — `8.8.8.8`
- Cloudflare DNS — `1.1.1.1`

Your ISP may also provide its own recursive resolver.

---

## Where it fits

The complete process looks like:

```
Your Computer
     │
     │ "What is www.example.com?"
     ▼
Recursive Resolver
     │
     ├──► Root Server
     │       │
     │       ▼
     │     .com TLD
     │       │
     │       ▼
     │   Authoritative DNS
     │       │
     │       ▼
     │   IP address
     │
     ▼
Your Computer
```

The important point is that **your computer normally doesn't need to contact the root, TLD, and authoritative servers itself**.

The recursive resolver does that work.

# Recursive vs Iterative Queries

Another important concept:

### Recursive query

The client tells the resolver:

> "Give me the final answer."

```
Client ──────► Recursive Resolver
                 │
                 │ does the work
                 ▼
              Final answer
```

### Iterative query

A DNS server essentially says:

> "I don't have the final answer, but here's where you should look next."

For example:

```
Resolver ──► Root
              │
              └──► "Ask .com"

Resolver ──► .com
              │
              └──► "Ask these authoritative servers"

Resolver ──► Authoritative
              │
              └──► "93.184.216.34"
```

So the resolver typically performs **iterative queries** to DNS hierarchy servers while providing a **recursive service** to the client.

# Common Recursive DNS Resolvers

Some well-known public resolvers:

| Provider          | IPv4      |
| ----------------- | --------- |
| Google Public DNS | `8.8.8.8` |
| Google Public DNS | `8.8.4.4` |
| Cloudflare        | `1.1.1.1` |
| Cloudflare        | `1.0.0.1` |
| Quad9             | `9.9.9.9` |


# DNS Records

A **DNS record** is an entry in DNS that tells the DNS system **how a domain name or hostname should be handled**.

Think of DNS records as the **actual data stored in a DNS zone**.

For example:

```
example.com
     │
     ├── A       → IPv4 address
     ├── AAAA    → IPv6 address
     ├── MX      → Mail server
     ├── NS      → Name server
     ├── CNAME   → Alias
     └── TXT     → Text information
```

---

# 1. A Record

**A = Address**

Maps a hostname to an **IPv4 address**.

```
example.com → 93.184.216.34
```

Example:

```
dig example.com A
```

Possible response:

```
example.com.    300    IN    A    93.184.216.34
```

### Used for

```
www.example.com → 192.0.2.10
api.example.com → 192.0.2.20
```

**Pentesting relevance:** A records can reveal the IP infrastructure associated with a target.

---

# 2. AAAA Record

Maps a hostname to an **IPv6 address**.

```
example.com → 2001:db8::10
```

Example:

```
dig example.com AAAA
```

Difference:

|Record|Address|
|---|---|
|A|IPv4|
|AAAA|IPv6|

**Pentesting relevance:** Don't ignore AAAA records. A target may have an IPv6 service that has different exposure or configuration from its IPv4 infrastructure.

---

# 3. CNAME Record

**CNAME = Canonical Name**

Creates an alias from one hostname to another hostname.

Example:

```
www.example.com → example.com
```

DNS:

```
www.example.com    CNAME    example.com
```

Then:

```
example.com        A        93.184.216.34
```

So:

```
www.example.com
       ↓ CNAME
example.com
       ↓ A
93.184.216.34
```

### Important

A CNAME points to a **hostname**, not directly to an IP.

### Pentesting relevance

CNAME records are particularly interesting during reconnaissance because they can reveal:

```
app.example.com
       ↓
something.cloud-provider.com
```

This can expose third-party infrastructure and, when misconfigured, potentially create **subdomain takeover** conditions.

---

# 4. MX Record

**MX = Mail Exchange**

Specifies the mail servers responsible for receiving email for a domain.

Example:

```
example.com    MX    10 mail.example.com
```

The number `10` is the **priority**.

Lower number = higher priority.

Example:

```
example.com
   │
   ├── MX 10 → mail1.example.com
   └── MX 20 → mail2.example.com
```

Query:

```
dig example.com MX
```

### Pentesting relevance

MX records can reveal:

- Email infrastructure
- Third-party email providers
- Organization technology
- Potential attack surface

---

# 5. NS Record

**NS = Name Server**

Specifies the authoritative DNS servers for a domain/zone.

Example:

```
example.com    NS    ns1.example-dns.com
example.com    NS    ns2.example-dns.com
```

Query:

```
dig example.com NS
```

These servers are authoritative for the domain's DNS zone.

### Remember

```
NS → Who is authoritative for this domain?
```

---

# 6. TXT Record

**TXT = Text**

Stores arbitrary text associated with a DNS name.

Example:

```
example.com    TXT    "some-value"
```

TXT records are commonly used for:

- Domain verification
- SPF
- Email security information
- Service configuration
- Ownership verification

For example:

```
dig example.com TXT
```

You might see:

```
"v=spf1 include:_spf.example.com ~all"
```

### Pentesting relevance

TXT records can reveal useful organizational information and email-security configuration.

---

# 7. SOA Record

**SOA = Start of Authority**

Contains administrative information about a DNS zone.

Example:

```
dig example.com SOA
```

It can contain information such as:

```
Primary name server
Responsible mailbox
Serial number
Refresh
Retry
Expire
Minimum/negative caching information
```

Conceptually:

```
example.com
     │
     └── SOA
          ├── Primary DNS server
          ├── Responsible party
          ├── Serial
          ├── Refresh
          ├── Retry
          └── Expire
```

The SOA record is important for understanding how a DNS zone is administered and replicated.

---

# 8. PTR Record

**PTR = Pointer**

Used for **reverse DNS**.

Normal DNS:

```
hostname → IP
```

PTR:

```
IP → hostname
```

Example:

```
93.184.216.34
       ↓
www.example.com
```

You can query it with:

```
dig -x 93.184.216.34
```

### Pentesting relevance

Reverse DNS can help identify:

- Server names
- Infrastructure naming conventions
- Hosting providers
- Potentially related systems

---

# 9. SRV Record

**SRV = Service**

Used to specify where a particular service is available.

Format conceptually:

```
_service._protocol.example.com
```

Example:

```
_ldap._tcp.example.com
```

might point to:

```
ldap.example.com:389
```

SRV records are common in environments using services such as:

- LDAP
- Kerberos
- SIP
- Microsoft Active Directory

### Pentesting relevance

SRV records can reveal internal service infrastructure, particularly in **Active Directory/DNS enumeration**.

---

# 10. CAA Record

**CAA = Certification Authority Authorization**

Specifies which Certificate Authorities (CAs) are authorized to issue TLS certificates for a domain.

Example:

```
example.com    CAA    0 issue "letsencrypt.org"
```

Meaning, roughly:

> This domain authorizes Let's Encrypt to issue certificates.

Query:

```
dig example.com CAA
```

# DNS TTL

**TTL = Time To Live.**

In DNS, TTL specifies **how long a DNS record may be cached before it should be queried again**.

It is expressed in **seconds**.

For example:

```
example.com.    300    IN    A    93.184.216.34
                ↑
               TTL
```

Here:

```
TTL = 300 seconds = 5 minutes
```

---

## Why does DNS need TTL?

Imagine millions of users repeatedly asking:

```
"What is the IP of example.com?"
```

Without caching:

```
User 1 ──► DNS
User 2 ──► DNS
User 3 ──► DNS
User 4 ──► DNS
...
```

This would generate enormous DNS traffic.

Instead, a recursive resolver can cache the answer:

```
                 DNS
                  │
                  ▼
          example.com
          93.184.216.34
             TTL 300
                  │
                  ▼
             DNS Cache
            ┌─────────┐
            │ 5 min   │
            └─────────┘
             ↙  ↓  ↘
          User User User
```

The resolver can reuse the cached answer while its TTL remains valid.

---

# Example

Suppose the authoritative DNS server returns:

```
example.com.    3600    IN    A    93.184.216.34
```

That means:

```
3600 seconds
= 60 minutes
= 1 hour
```

A recursive resolver can cache that record for up to approximately one hour.

After the TTL expires, it needs to obtain a fresh answer.

```
Initial lookup
     ↓
Cache for 3600 seconds
     ↓
TTL expires
     ↓
Query DNS again
     ↓
New TTL
```

---

# TTL Countdown

Suppose:

```
TTL = 300
```

When the resolver initially caches it:

```
300 seconds
```

After 100 seconds:

```
200 seconds remaining
```

After another 150 seconds:

```
50 seconds remaining
```

After 50 more seconds:

```
0
```

The cached record is considered expired and the resolver must refresh it when needed.

---

# TTL and DNS Changes

Suppose a company changes:

```
example.com → 10.10.10.10
```

to:

```
example.com → 20.20.20.20
```

If the old record had:

```
TTL = 86400
```

that's:

```
86400 seconds = 24 hours
```

Some recursive resolvers may continue serving the old cached answer until its TTL expires.

Therefore:

> **Changing a DNS record does not necessarily mean every user immediately sees the new record.**

---

# High TTL vs Low TTL

|TTL|Typical effect|
|---|---|
|**Low TTL**|Changes propagate through caches faster, but causes more DNS queries|
|**High TTL**|Better caching and fewer DNS queries, but changes can take longer to propagate|

For example:

```
TTL 60
```

≈ 1 minute

```
TTL 300
```

≈ 5 minutes

```
TTL 3600
```

≈ 1 hour

```
TTL 86400
```

≈ 24 hours


# Reverse DNS

**Reverse DNS (rDNS)** is the process of finding a **hostname/domain name from an IP address**.

Normal DNS works:

```
Domain → IP
```

Reverse DNS works:

```
IP → Domain/Hostname
```

---

## Normal DNS vs Reverse DNS

### Forward DNS

You start with:

```
www.example.com
```

DNS finds:

```
93.184.216.34
```

```
www.example.com
       ↓
      DNS
       ↓
93.184.216.34
```

This usually uses an **A** record for IPv4 or **AAAA** for IPv6.

---

### Reverse DNS

You start with:

```
93.184.216.34
```

DNS tries to find:

```
www.example.com
```

```
93.184.216.34
       ↓
   Reverse DNS
       ↓
www.example.com
```

Reverse DNS uses a **PTR record**.

---

# PTR Record

**PTR = Pointer record**

It maps an IP address to a hostname.

For example:

```
93.184.216.34
       ↓
www.example.com
```

The corresponding PTR record conceptually looks like:

```
34.216.184.93.in-addr.arpa.
        PTR
www.example.com.
```

Notice that the IPv4 address is **reversed**.

---

# Why Is the IP Reversed?

IPv4:

```
93.184.216.34
```

becomes:

```
34.216.184.93
```

and is placed under:

```
in-addr.arpa
```

So:

```
34.216.184.93.in-addr.arpa
```

is the DNS name used for the reverse lookup.

# Who Controls PTR Records?

This is an important distinction.

For normal DNS:

```
example.com
```

the domain owner controls its DNS zone.

For reverse DNS:

```
IP → hostname
```

the organization controlling the relevant **IP address block** generally controls the corresponding reverse DNS zone.

For example, if a cloud provider owns an IP range, the provider may control the reverse DNS delegation, although customers may be allowed to configure PTR records for allocated addresses.

# Reverse DNS for IPv6

IPv6 reverse DNS uses:

```
ip6.arpa
```

instead of:

```
in-addr.arpa
```

For IPv4:

```
in-addr.arpa
```

For IPv6:

```
ip6.arpa
```

You normally don't need to manually construct the IPv6 reverse name because tools such as `dig -x` handle it.

Reverse DNS can provide information such as:

```
IP address
    ↓
server.example.com
```

The hostname might reveal:

- Organization
- Server purpose
- Hosting provider
- Geographic/location naming
- Infrastructure naming conventions
- Mail server identity

# DNS Propagation

**DNS propagation** is the process by which a **DNS record change becomes visible to different DNS resolvers and users across the Internet**.

For example, suppose:

```
example.com → 203.0.113.10
```

You change it to:

```
example.com → 203.0.113.20
```

Different DNS resolvers may temporarily return different answers because they have **cached the old record**.

---

## Why does this happen?

The main reason is **DNS caching + TTL**.

Suppose the old record is:

```
example.com    3600    A    203.0.113.10
```

The TTL is:

```
3600 seconds = 1 hour
```

A recursive resolver that cached the old answer may continue using it until the TTL expires.

Meanwhile, a resolver that has already refreshed the record may return:

```
203.0.113.20
```

So temporarily:

```
User A → Resolver A → 203.0.113.10
User B → Resolver B → 203.0.113.20
```

---

# DNS Propagation Example

Imagine you change:

```
www.example.com
       ↓
203.0.113.10
```

to:

```
www.example.com
       ↓
203.0.113.20
```

At the time of the change:

```
Authoritative DNS
        │
        ▼
203.0.113.20
```

But some recursive resolvers still have:

```
Cache
──────
203.0.113.10
```

Therefore:

```
                 Authoritative DNS
                       │
                       │ NEW
                       ▼
                  203.0.113.20

       ┌────────────────┴────────────────┐
       ▼                                 ▼
Resolver A                         Resolver B
cached OLD                         refreshed
203.0.113.10                       203.0.113.20
       │                                 │
       ▼                                 ▼
   User A                             User B
```

As caches expire, more resolvers obtain the new value.

Eventually:

```
All relevant caches
       ↓
New DNS record
```

---

# TTL Controls How Long Caches Can Keep the Old Answer

Suppose the old record has:

```
TTL = 86400
```

That's:

```
24 hours
```

A resolver that cached the record shortly before you changed it could potentially continue using that cached response for much of that remaining TTL.

If instead:

```
TTL = 60
```

the cache lifetime is only about:

```
1 minute
```

So changes can generally become visible to caching resolvers sooner.

---

# Is DNS Propagation Actually "Sending the Record Everywhere"?

Not really.

This is a common misconception.

DNS doesn't normally work like:

```
Change DNS
   ↓
Push new record
   ↓
Every DNS server on Earth
```

Instead:

```
Authoritative DNS
       ↓
New answer

Recursive resolvers
       ↓
Use cached answer until TTL expires
       ↓
Query authoritative DNS again
       ↓
Receive new answer
```

So **DNS propagation is primarily the gradual expiration and refresh of cached DNS data**, rather than a global push mechanism.

---

# Example with TTL

Suppose:

```
Old:
example.com → 10.0.0.1
TTL = 300
```

A resolver caches it at:

```
12:00
```

You change the DNS record at:

```
12:01
```

That resolver may still have:

```
10.0.0.1
```

until its cached TTL expires.

At approximately:

```
12:05
```

it can refresh and discover:

```
10.0.0.2
```

The exact timing depends on when the resolver cached the old response and DNS behavior/configuration.

# Wildcard DNS

A **Wildcard DNS record** is a DNS record that can provide an answer for **any otherwise-unmatched subdomain** under a particular DNS name.

The wildcard symbol is:

```
*
```

### Example

Suppose a domain has:

```
*.example.com    A    203.0.113.10
```

Then DNS can resolve arbitrary names such as:

```
abc.example.com       → 203.0.113.10
test.example.com      → 203.0.113.10
random.example.com    → 203.0.113.10
anything.example.com  → 203.0.113.10
```

provided there isn't a more specific applicable DNS record.

---

# Normal DNS vs Wildcard DNS

### Normal DNS

You explicitly define each hostname:

```
www.example.com    A    203.0.113.10
api.example.com    A    203.0.113.20
mail.example.com   A    203.0.113.30
```

If you query:

```
random.example.com
```

there may be no answer.

---

### Wildcard DNS

Instead:

```
*.example.com    A    203.0.113.10
```

Now:

```
www.example.com       → 203.0.113.10
random.example.com    → 203.0.113.10
abc.example.com       → 203.0.113.10
```

The wildcard acts as a **fallback** for names that don't have their own applicable record.

---

# How It Works

Imagine:

```
example.com
│
├── www       → 203.0.113.20
├── api       → 203.0.113.30
└── *         → 203.0.113.10
```

Now:

```
www.example.com
       ↓
Specific record exists
       ↓
203.0.113.20
```

But:

```
random.example.com
       ↓
No specific record
       ↓
Wildcard matches
       ↓
203.0.113.10
```

So the wildcard doesn't necessarily override an explicitly defined hostname.

---

# Important Example

Suppose:

```
*.example.com       A    203.0.113.10
api.example.com     A    203.0.113.20
```

Queries:

|Query|Result|
|---|---|
|`api.example.com`|`203.0.113.20`|
|`test.example.com`|`203.0.113.10`|
|`abc.example.com`|`203.0.113.10`|
|`random.example.com`|`203.0.113.10`|

The specific record for `api` takes precedence over the wildcard.

---

# Wildcard Doesn't Mean "Everything"

A common misunderstanding is:

> `*.example.com` matches every possible DNS name under `example.com`.

Not exactly.

It applies to **otherwise-unmatched names at the relevant DNS level**, subject to DNS wildcard rules.

For example:

```
*.example.com
```

matches names such as:

```
test.example.com
api2.example.com
```

But DNS wildcard behavior becomes more nuanced with deeper names:

```
a.b.example.com
```

A wildcard at `*.example.com` should not simply be thought of as a universal pattern matching arbitrary depth.

---

# Wildcard DNS vs Wildcard Certificate

Don't confuse these two.

### Wildcard DNS

```
*.example.com → 203.0.113.10
```

Controls DNS resolution.

### Wildcard TLS certificate

```
*.example.com
```

Allows a certificate to cover names such as:

```
www.example.com
api.example.com
```

They are separate concepts.


# Wildcard DNS Detection Concept

During reconnaissance:

```
Find candidate subdomains
        ↓
Resolve them
        ↓
Check random nonexistent hostname
        ↓
Does it also resolve?
       / \
     YES  NO
      │    │
      ▼    ▼
Wildcard  Normal
likely    DNS
```


# DNS Misconfiguration

A **DNS misconfiguration** happens when DNS records, DNS servers, or DNS settings are configured incorrectly or insecurely.

For bug bounty and penetration testing, DNS misconfigurations are important because they can expose **internal infrastructure, forgotten services, mail systems, cloud resources, or takeover opportunities**.

---

## 1. Common DNS Misconfigurations

|Misconfiguration|What happens|Security impact|
|---|---|---|
|**Dangling CNAME**|CNAME points to a deleted/unclaimed external resource|Possible subdomain takeover|
|**Open DNS Zone Transfer**|Anyone can request the entire DNS zone|Information disclosure|
|**Wildcard DNS**|Non-existent subdomains resolve to an IP|False positives during enumeration|
|**Incorrect A/AAAA record**|Domain points to wrong server|Exposure/misrouting|
|**Stale DNS records**|Old infrastructure remains in DNS|Forgotten assets may be exposed|
|**Exposed internal DNS records**|Internal hostnames/IPs are publicly resolvable|Information disclosure|
|**DNSSEC misconfiguration**|DNSSEC is incorrectly implemented|Integrity/availability issues|
|**Weak NS configuration**|Poorly configured name servers|Availability/delegation risks|
|**Missing SPF/DKIM/DMARC**|Email DNS controls are absent/weak|Email spoofing/phishing risk|
|**Incorrect MX records**|Mail points to wrong/unintended server|Mail interception/delivery issues|
|**Excessive TXT information**|Sensitive infrastructure information exposed|Information disclosure|
|**Unintended DNS recursion**|Resolver answers recursive queries from unauthorized users|DNS abuse/amplification risk|

---

# 2. Zone Transfer Misconfiguration

A DNS **zone transfer** is normally used to replicate DNS zone data between authoritative DNS servers.

The problem occurs when a server allows unauthorized users to perform an `AXFR`.

For example:

```
dig AXFR example.com @ns1.example.com
```

A vulnerable server might reveal:

```
dev.example.com
admin.example.com
vpn.example.com
internal.example.com
mail.example.com
test.example.com
```

Instead of discovering these individually, you may obtain a large portion of the zone at once.

### Why it matters

It can reveal:

- Internal hostnames
- Development systems
- VPN endpoints
- Mail servers
- Staging environments
- Infrastructure naming conventions

**Pentesting impact:** Information disclosure / attack-surface discovery.

Only test this against domains you are authorized to assess.

---

# 3. Dangling CNAME

One of the most important DNS issues for bug bounty.

Suppose:

```
blog.example.com
        |
        CNAME
        ↓
example.github.io
```

Later, the company deletes the corresponding GitHub resource but forgets to remove:

```
blog.example.com → example.github.io
```

The DNS record is now **dangling**.

Conceptually:

```
blog.example.com
       ↓
CNAME
       ↓
Deleted cloud resource
       ↓
Potentially claimable by attacker
```

If the external provider allows someone else to claim that resource, the attacker may be able to control:

```
blog.example.com
```

This is commonly called a **subdomain takeover**.

### Important distinction

```
Dangling CNAME
      ↓
Potential takeover
```

But:

```
CNAME exists
      ≠
Takeover is possible
```

You need to verify that the referenced resource is actually **unclaimed and claimable** according to the provider's rules.

---

# 4. Wildcard DNS Misconfiguration

Example:

```
*.example.com → 203.0.113.10
```

Now:

```
abc.example.com
random.example.com
testing123.example.com
```

may all resolve to the same IP.

This can cause a major problem during subdomain enumeration.

Suppose your tool discovers:

```
admin.example.com
random123.example.com
xyz987.example.com
```

You might think all three are legitimate hosts.

But:

```
dig random-nonexistent-987654.example.com
```

returns:

```
203.0.113.10
```

That suggests wildcard DNS.

Therefore:

```
Enumeration
     ↓
DNS resolution
     ↓
Wildcard detection
     ↓
Filter wildcard results
     ↓
Investigate real hosts
```

### Important

Wildcard DNS itself is **not automatically a vulnerability**.

It becomes relevant because it can:

- Create false positives
- Complicate asset discovery
- Potentially interact with application routing or security controls

---

# 5. Stale DNS Records

Example:

```
old-admin.example.com → 198.51.100.50
```

The server was retired months ago, but the DNS record remains.

This creates a **stale DNS record**.

Possible situations:

```
DNS
 ↓
Old AWS instance
 ↓
Instance deleted
```

or:

```
DNS
 ↓
Old SaaS service
 ↓
Account/resource abandoned
```

The second situation can potentially become a **subdomain takeover** if the external resource is claimable.

---

# 6. Internal DNS Information Exposure

A company might accidentally expose names such as:

```
dc01.internal.example.com
db01.internal.example.com
vpn.internal.example.com
jenkins.internal.example.com
dev.internal.example.com
```

Even if these hosts aren't directly accessible from the Internet, DNS can disclose useful infrastructure information.

For example:

```
10.10.20.15 db01.internal.example.com
10.10.20.20 dc01.internal.example.com
```

This can reveal:

- Naming conventions
- Server roles
- Internal architecture
- IP ranges
- Development environments

This is usually an **information disclosure** issue rather than an immediate remote compromise.

---

# 7. Email DNS Misconfiguration

Several DNS records control email security.

Important ones:

```
MX
SPF
DKIM
DMARC
```

For example:

```
dig example.com MX
dig example.com TXT
```

Weak or missing email security can contribute to:

- Email spoofing
- Phishing
- Domain impersonation
- Poor mail authentication

For example, DMARC helps receiving mail systems determine what to do when messages fail authentication checks.

---

# 8. DNSSEC Misconfiguration

**DNSSEC** adds cryptographic authentication to DNS data.

Conceptually:

```
Normal DNS:

User → DNS → "example.com = 1.2.3.4"


DNSSEC:

User → DNS → answer + cryptographic validation
```

Misconfigured DNSSEC can cause:

- DNS resolution failures
- Validation failures
- Availability problems
- Incorrect delegation/signing configuration

DNSSEC is more about **DNS data integrity and authentication** than confidentiality.

---

# 9. Open Recursive Resolver

A DNS resolver can perform recursion:

```
Client
  ↓
Recursive Resolver
  ↓
Root
  ↓
TLD
  ↓
Authoritative
```

If recursion is unnecessarily exposed to the Internet, the resolver may be abused for:

- DNS amplification
- Reflection attacks
- Unauthorized recursive queries
- Resource consumption

This is generally an infrastructure/security configuration issue.

---

# 10. How a Pentester Checks DNS

A basic workflow:

```
              DNS Testing
                   │
        ┌──────────┴──────────┐
        ↓                     ↓
   Find DNS records       Find NS servers
        │                     │
        ↓                     ↓
 A / AAAA / CNAME        Authoritative DNS
 MX / TXT / NS / etc.          │
        │                       ↓
        └──────────┬────────────┘
                   ↓
           Check misconfigurations
                   │
       ┌───────────┼────────────┐
       ↓           ↓            ↓
 Zone Transfer  Dangling CNAME  Wildcard
       ↓           ↓            ↓
 Internal DNS   Takeover?    False positives
       ↓
 Email DNS
```

Useful commands:

```
dig example.com A
dig example.com AAAA
dig example.com CNAME
dig example.com MX
dig example.com NS
dig example.com TXT
dig example.com SOA
```

Find authoritative servers:

```
dig example.com NS
```

Test zone transfer **only when authorized**:

```
dig AXFR example.com @ns1.example.com
```

Check wildcard behavior:

```
dig random-nonexistent-987654.example.com
```

Check reverse DNS:

```
dig -x 203.0.113.10
```