
---
`whois` is a command-line utility used to query **WHOIS registration information** for domains, IP addresses, and certain Internet resources.

In pentesting, WHOIS is mainly used during **passive reconnaissance / OSINT** to gather information such as:

- Domain registration information
- Registrar
- Registration/expiration dates
- Nameservers
- Domain status
- Registrant information, when publicly available
- IP/network ownership information
- Autonomous System / organization information, depending on the WHOIS service

> WHOIS data is often privacy-protected, redacted, or incomplete. Treat it as reconnaissance data, not authoritative proof of ownership.

---

# 1. Installation

### Kali Linux / Debian / Ubuntu

```
sudo apt update
sudo apt install whois
```

Check installation:

```
whois --version
```

or:

```
which whois
```

---

# 2. Basic Syntax

The fundamental syntax is:

```
whois [OPTIONS] TARGET
```

Example:

```
whois example.com
```

Here:

```
whois       → program
example.com → target
```

---

# 3. Basic Domain Lookup

```
whois example.com
```

Typical information may include:

```
Domain Name
Registrar
Creation Date
Updated Date
Expiration Date
Domain Status
Name Servers
DNSSEC
```

For example:

```
whois example.com
```

You might see:

```
Domain Name: EXAMPLE.COM
Registrar: Example Registrar
Creation Date: ...
Expiration Date: ...
Name Server: NS1.EXAMPLE.COM
Name Server: NS2.EXAMPLE.COM
```

---

# 4. Query an IP Address

WHOIS isn't limited to domains.

```
whois 8.8.8.8
```

This can return information about the organization/network associated with the IP.

Typical fields include:

```
NetRange
CIDR
Organization
NetName
Country
OrgName
OrgTechEmail
```

For example:

```
whois 8.8.8.8
```

may identify the network/organization responsible for that address range.

---

# 5. Domain vs IP WHOIS

### Domain

```
whois example.com
```

You are generally investigating:

```
Domain
  ↓
Registrar
  ↓
Registration
  ↓
Nameservers
  ↓
Status
```

### IP

```
whois 8.8.8.8
```

You are generally investigating:

```
IP
  ↓
Network range
  ↓
Organization
  ↓
ASN / allocation information
  ↓
Regional Internet Registry
```

---

# 6. Useful Options

The exact options can vary slightly between WHOIS implementations.

Always check:

```
whois --help
```

or:

```
man whois
```

Common options include:

|Option|Purpose|
|---|---|
|`-h`|Specify WHOIS server|
|`-p`|Specify WHOIS server port|
|`-H`|Hide legal disclaimers|
|`--help`|Display help|
|`--version`|Show version|

---

# 7. `-h` — Specify WHOIS Server

Syntax:

```
whois -h SERVER TARGET
```

Example:

```
whois -h whois.verisign-grs.com example.com
```

Meaning:

```
-h
 ↓
Use a particular WHOIS server

whois.verisign-grs.com
 ↓
WHOIS server

example.com
 ↓
Target
```

This is useful when you specifically want to query a particular WHOIS service.

---

# 8. `-p` — Specify Port

Syntax:

```
whois -p PORT TARGET
```

Example:

```
whois -p 43 example.com
```

WHOIS traditionally uses:

```
TCP/43
```

You normally won't need to specify this because the client uses the standard port automatically.

---

# 9. `-H` — Hide Legal Disclaimer

Some WHOIS responses contain lengthy legal/usage disclaimers.

```
whois -H example.com
```

This can make output easier to read.

---

# 10. Save WHOIS Output

Very useful during pentesting.

```
whois example.com > whois.txt
```

Now:

```
cat whois.txt
```

or:

```
less whois.txt
```

You can also append:

```
whois example.com >> recon.txt
```

---

# 11. Search WHOIS Output

You can pipe the output into Linux tools.

### Search for registrar

```
whois example.com | grep -i registrar
```

### Search for nameservers

```
whois example.com | grep -i "name server"
```

### Search for dates

```
whois example.com | grep -Ei "creation|created|updated|expiration|expiry"
```

### Search for organization

```
whois 8.8.8.8 | grep -Ei "orgname|organization|netname"
```

---

# 12. `grep` + WHOIS

This combination is particularly useful.

```
whois example.com | grep -i "domain"
```

```
whois example.com | grep -i "status"
```

```
whois example.com | grep -i "registrar"
```

```
whois example.com | grep -i "server"
```

Case-insensitive search:

```
whois example.com | grep -i "registrar"
```

The `-i` means:

```
ignore case
```

---

# 13. Extract Nameservers

```
whois example.com | grep -i "name server"
```

Possible output:

```
Name Server: NS1.EXAMPLE.COM
Name Server: NS2.EXAMPLE.COM
```

You can then investigate those nameservers separately using DNS tools.

For example:

```
dig NS example.com
```

---

# 14. Domain Status

Search:

```
whois example.com | grep -i status
```

You may see statuses such as:

```
clientTransferProhibited
clientUpdateProhibited
clientDeleteProhibited
```

These are registry/registrar domain-status codes.

Don't automatically interpret a status code as a security vulnerability.

---

# 15. Registration Dates

```
whois example.com | grep -Ei "creation|created"
```

Expiration:

```
whois example.com | grep -Ei "expiration|expiry"
```

Updated:

```
whois example.com | grep -Ei "updated|last update"
```

---

# 16. IP WHOIS Reconnaissance

Suppose DNS gives you:

```
example.com → 203.0.113.10
```

You can investigate the IP allocation:

```
whois 203.0.113.10
```

Then:

```
whois 203.0.113.10 | grep -Ei "org|netname|cidr|range"
```

This can help identify the organization/network associated with the address.

---

# 17. WHOIS + DNS Workflow

WHOIS is more useful when combined with other passive-recon tools.

A basic workflow:

```
Domain
   │
   ├── WHOIS
   │     ├── Registrar
   │     ├── Nameservers
   │     └── Registration data
   │
   └── DNS
         ├── A
         ├── AAAA
         ├── MX
         ├── NS
         └── TXT
```

For example:

### Step 1

```
whois example.com
```

### Step 2

```
dig NS example.com
```

### Step 3

```
dig A example.com
```

### Step 4

```
dig MX example.com
```

### Step 5

```
dig TXT example.com
```

---

# 18. WHOIS + `dig`

Find nameservers:

```
whois example.com | grep -i "name server"
```

Then:

```
dig NS example.com
```

Find IP:

```
dig A example.com
```

Then investigate the IP:

```
whois <IP>
```

Example:

```
whois 203.0.113.10
```

So the workflow becomes:

```
example.com
     ↓
   WHOIS
     ↓
Nameservers
     ↓
    DNS
     ↓
    IP
     ↓
 IP WHOIS
     ↓
Network/Organization
```

---

# 19. WHOIS + Reverse DNS

After obtaining an IP:

```
whois 203.0.113.10
```

Then:

```
dig -x 203.0.113.10
```

or:

```
host 203.0.113.10
```

This can provide a reverse-DNS hostname if one exists.

---

# 20. Query Multiple Domains

WHOIS itself generally handles one target per invocation, so use a shell loop.

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
    whois "$domain"
done < domains.txt
```

Better organized:

```
while read domain; do
    echo "===== $domain ====="
    whois "$domain"
done < domains.txt
```

Save everything:

```
while read domain; do
    echo "===== $domain ====="
    whois "$domain"
done < domains.txt > whois-results.txt
```

---

# 21. Simple Recon Script

For an authorized assessment:

```
#!/bin/bash

domain="$1"

echo "===== WHOIS ====="
whois "$domain"

echo
echo "===== NAMESERVERS ====="
whois "$domain" | grep -i "name server"
```

Run:

```
chmod +x recon.sh
```

Then:

```
./recon.sh example.com
```

---

# 22. Common Mistake: URL Instead of Domain

Don't normally do:

```
whois https://example.com/login
```

Use:

```
whois example.com
```

WHOIS operates on domain/resource identifiers, not web URLs.

---

# 23. Common Mistake: Using a Subdomain

For:

```
www.example.com
```

WHOIS generally concerns the registered domain:

```
whois example.com
```

Rather than:

```
whois www.example.com
```

For DNS information about the subdomain, use:

```
dig www.example.com
```

---

# 24. Privacy-Redacted WHOIS

Modern WHOIS data frequently looks like:

```
Registrant Organization: REDACTED
Registrant Name: REDACTED
Registrant Email: REDACTED
```

This does **not** mean WHOIS failed.

It means the registrar/registry isn't publicly exposing that information.

You can still potentially obtain:

```
Registrar
Creation date
Expiration date
Nameservers
Domain status
DNSSEC
Registry information
```

depending on the domain and registry.

---

# 25. WHOIS Is Not the Same as DNS

This distinction is important.

### WHOIS

Answers:

> **Who/which organization is associated with this Internet resource, and what registration/allocation information is available?**

### DNS

Answers:

> **How does this domain resolve to Internet services?**

Example:

```
WHOIS
example.com
   ↓
Registrar
Nameservers
Registration data
```

while:

```
DNS
example.com
   ↓
A → IP
MX → Mail server
NS → Nameserver
TXT → Text records
```

You generally use both during reconnaissance.

---

# 26. WHOIS vs RDAP

Modern Internet registration data is increasingly provided through **RDAP (Registration Data Access Protocol)**.

WHOIS is the older protocol.

Conceptually:

```
WHOIS
  ↓
Legacy registration lookup

RDAP
  ↓
Modern structured registration lookup
```

For modern reconnaissance, knowing both is useful.

---

# 27. Professional Passive-Recon Workflow

For an authorized domain:

```
             TARGET
                │
                ▼
             WHOIS
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
    Registrar  Dates   Nameservers
                         │
                         ▼
                        DNS
                         │
              ┌──────────┼──────────┐
              ▼          ▼          ▼
              A         MX         TXT
              │
              ▼
             IP
              │
              ▼
          IP WHOIS
              │
              ▼
       Network / Org / CIDR
```

The important point is that **WHOIS is usually the starting point, not the complete reconnaissance process**.

---

# 28. Quick Reference

```
# Basic domain lookup
whois example.com

# IP lookup
whois 8.8.8.8

# Specific WHOIS server
whois -h whois.verisign-grs.com example.com

# Specify port
whois -p 43 example.com

# Hide disclaimer
whois -H example.com

# Save output
whois example.com > whois.txt

# Search registrar
whois example.com | grep -i registrar

# Search nameservers
whois example.com | grep -i "name server"

# Search dates
whois example.com | grep -Ei "creation|created|updated|expiration|expiry"

# Search organization for IP
whois 8.8.8.8 | grep -Ei "orgname|organization|netname"

# Process domains from file
while read domain; do
    whois "$domain"
done < domains.txt
```

### What to remember

```
whois DOMAIN
     │
     ├── Registrar
     ├── Registration dates
     ├── Domain status
     ├── Nameservers
     └── Registration information

whois IP
     │
     ├── Organization
     ├── Network range
     ├── CIDR
     └── Allocation information
```