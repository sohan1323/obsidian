
---
[OWASP Amass — Official GitHub Repository](https://github.com/owasp-amass/amass?utm_source=chatgpt.com)

`Amass` is an OWASP tool for **attack-surface mapping, external asset discovery, DNS enumeration, and network mapping**. It combines OSINT/data sources with DNS enumeration and, when explicitly enabled, active reconnaissance. [GitHub](https://github.com/owasp-amass/amass?utm_source=chatgpt.com)

For your red-team learning, think of Amass as a **larger reconnaissance framework**, whereas `host`, `nslookup`, and `dig` are individual DNS utilities.

> **Scope:** use active enumeration, brute force, DNS queries, and network probing only against systems you are authorized to test.

---

# 1. Amass Architecture

The main Amass commands are:

```
amass
 │
 ├── intel    → organization intelligence
 │
 ├── enum     → DNS / subdomain enumeration
 │
 ├── viz      → visualize collected data
 │
 ├── track    → compare enumerations
 │
 └── db       → manage enumeration database
```

OWASP describes `intel` as organizational intelligence gathering and `enum` as DNS enumeration/network mapping; the database stores the resulting investigation data. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 2. Installation

On Kali, Amass is available through the distribution. OWASP also provides prebuilt releases and Docker installation methods. [GitHub](https://github.com/owasp-amass/amass/wiki/Installation-Guide?utm_source=chatgpt.com)

Check first:

```
amass -version
```

Help:

```
amass -help
```

Subcommand help:

```
amass enum -help
```

```
amass intel -help
```

```
amass db -help
```

```
amass viz -help
```

---

# 3. The Most Important Command

For normal subdomain enumeration:

```
amass enum -d example.com
```

This is the command you should memorize first.

Breakdown:

```
amass
  ↓
enum
  ↓
enumeration mode
  ↓
-d example.com
  ↓
target domain
```

OWASP's user guide gives this as the basic Amass enumeration example. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 4. Basic Enumeration

```
amass enum -d example.com
```

Amass gathers information about the target namespace and performs DNS enumeration/network mapping according to its configured sources and mode. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

Possible output:

```
api.example.com
dev.example.com
mail.example.com
vpn.example.com
www.example.com
```

The exact results depend on available data sources, DNS visibility, configuration, and the target.

---

# 5. `-d` — Target Domain

Syntax:

```
amass enum -d DOMAIN
```

Example:

```
amass enum -d example.com
```

Multiple domains can be supplied:

```
amass enum -d example.com,example.org
```

You can also use a file:

```
amass enum -df domains.txt
```

where:

```
example.com
example.org
example.net
```

---

# 6. Passive Enumeration

This is extremely important.

```
amass enum -passive -d example.com
```

or:

```
amass enum --passive -d example.com
```

Passive mode obtains information from data sources without performing the active DNS/network techniques associated with normal/active enumeration. OWASP documents `--passive` specifically for purely passive execution. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

### When learning recon

Start with:

```
amass enum -passive -d example.com
```

before moving to active enumeration.

---

# 7. Active Enumeration

```
amass enum -active -d example.com
```

You can specify ports:

```
amass enum -active -d example.com -p 80,443,8080
```

OWASP documents active mode as enabling active reconnaissance methods and port selection. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

Conceptually:

```
Passive
   ↓
Public information
   ↓
DNS/data sources

Active
   ↓
Passive information
   +
DNS/network interaction
   +
additional active discovery
```

Use active mode only when the engagement permits it.

---

# 8. Passive vs Normal vs Active

Think of the modes as:

```
                 Amass enum
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Passive     Normal      Active
          │          │            │
          ▼          ▼            ▼
      OSINT/data   DNS +       Additional
      sources      validation   active recon
```

### Passive

```
amass enum -passive -d example.com
```

### Normal

```
amass enum -d example.com
```

### Active

```
amass enum -active -d example.com
```

The exact behavior depends on the Amass version and configuration. [GitHub](https://github.com/JohnEarle/amass-develop/blob/master/doc/user_guide.md?utm_source=chatgpt.com)

---

# 9. Show IP Addresses — `-ip`

```
amass enum -ip -d example.com
```

Example conceptually:

```
api.example.com    203.0.113.10
mail.example.com   203.0.113.20
www.example.com    203.0.113.30
```

This is useful because you can immediately pivot from:

```
hostname
   ↓
IP
```

into:

```
whois <IP>
```

or:

```
dig -x <IP>
```

---

# 10. IPv4 Only

```
amass enum -ipv4 -d example.com
```

This displays discovered IPv4 addresses.

---

# 11. IPv6 Only

```
amass enum -ipv6 -d example.com
```

Useful when assessing IPv6 exposure.

---

# 12. Show Data Sources — `-src`

This is one of my recommended options while learning.

```
amass enum -src -d example.com
```

Instead of just seeing:

```
api.example.com
```

you can also understand **where Amass obtained the discovery**.

Conceptually:

```
api.example.com    [source]
```

OWASP documents `-src` for printing data sources associated with discovered names. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

This is extremely useful for understanding OSINT provenance.

---

# 13. Combine `-src` and `-ip`

```
amass enum -src -ip -d example.com
```

Now you're asking for:

```
hostname
+
source
+
IP
```

This is a very useful reconnaissance command.

---

# 14. Save Results — `-o`

Save discovered names:

```
amass enum -d example.com -o amass.txt
```

Then:

```
cat amass.txt
```

or:

```
less amass.txt
```

This is useful for passing results to other tools.

For example:

```
amass enum -passive -d example.com -o subdomains.txt
```

Then:

```
cat subdomains.txt
```

---

# 15. JSON Output — `-json`

Amass supports JSON output:

```
amass enum -d example.com -json results.json
```

This is useful when integrating Amass into automation or a larger reconnaissance pipeline.

---

# 16. Multiple Output Formats — `-oA`

The documented `-oA` option provides a path prefix for naming output files. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

Example:

```
amass enum -d example.com -oA amass_scan
```

This is convenient when you want a consistent output naming scheme.

---

# 17. Timeout — `-timeout`

Specify how long enumeration should run:

```
amass enum -d example.com -timeout 30
```

Meaning:

```
30
 ↓
minutes
```

OWASP documents `-timeout` as the number of minutes to execute enumeration. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

For example:

```
amass enum -passive -d example.com -timeout 10
```

---

# 18. DNS Resolvers — `-r`

You can specify preferred DNS resolvers:

```
amass enum -d example.com -r 8.8.8.8
```

Multiple:

```
amass enum -d example.com -r 8.8.8.8,1.1.1.1
```

The documented syntax allows preferred resolver IPs and supports multiple uses. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 19. Resolver File — `-rf`

Create:

```
resolvers.txt
```

Example:

```
8.8.8.8
1.1.1.1
9.9.9.9
```

Then:

```
amass enum -d example.com -rf resolvers.txt
```

This is useful when you want to control the resolver pool.

---

# 20. DNS Query Concurrency — `-max-dns-queries`

You can control the maximum number of concurrent DNS queries:

```
amass enum -d example.com -max-dns-queries 100
```

OWASP documents this option for controlling concurrent DNS queries. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

For a lab:

```
amass enum -d example.com -max-dns-queries 200
```

Higher isn't automatically better; DNS providers and network conditions can make aggressive settings counterproductive.

---

# 21. Brute-Force Subdomains — `-brute`

Amass can perform DNS brute-force enumeration:

```
amass enum -brute -d example.com
```

Conceptually:

```
Wordlist
   │
   ├── admin
   ├── dev
   ├── api
   ├── vpn
   ├── mail
   └── test
        │
        ▼
admin.example.com
dev.example.com
api.example.com
...
```

OWASP documents `-brute` as enabling brute-force subdomain enumeration. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

This generates DNS traffic, so treat it as active reconnaissance.

---

# 22. Custom Wordlist — `-w`

Use your own wordlist:

```
amass enum -brute -w wordlist.txt -d example.com
```

Example `wordlist.txt`:

```
admin
api
dev
test
staging
vpn
mail
portal
```

Amass tests combinations against the target domain.

---

# 23. Recursive Brute Force

Amass can recursively investigate discovered subdomains.

Example:

```
amass enum -brute -d example.com -min-for-recursive 2
```

`-min-for-recursive` controls how many labels must be observed before recursive brute forcing is triggered. OWASP documents the default as `1`. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

Conceptually:

```
dev.example.com
      ↓
discovered
      ↓
try deeper names
      ↓
test.dev.example.com
api.dev.example.com
...
```

---

# 24. Disable Recursive Brute Force

```
amass enum -brute -norecursive -d example.com
```

Useful when you want to control enumeration scope and reduce DNS activity.

---

# 25. Altered Names

Amass can generate altered names from discovered names.

Depending on your installed version:

```
amass enum -alts -d example.com
```

You can inspect:

```
amass enum -help
```

for the currently supported alteration options.

**Version note:** the current v5 development/release line has had changes/issues around alteration flags, so don't blindly rely on older tutorials; verify your installed version's behavior with `amass enum -help`. [GitHub](https://github.com/owasp-amass/amass/issues/1140?utm_source=chatgpt.com)

---

# 26. Custom Alteration Wordlist — `-aw`

Where supported:

```
amass enum -alts -aw alterations.txt -d example.com
```

Example:

```
dev
prod
stage
internal
old
new
```

This can generate additional candidate names from discovered infrastructure.

---

# 27. Known Names File — `-nf`

Suppose you already discovered subdomains with another tool:

```
known.txt
```

Example:

```
api.example.com
dev.example.com
vpn.example.com
```

Feed them to Amass:

```
amass enum -d example.com -nf known.txt
```

This is particularly useful when combining:

```
theHarvester
      ↓
subdomains
      ↓
Amass
      ↓
additional enumeration
```

---

# 28. Blacklist — `-bl`

Exclude a specific name:

```
amass enum -d example.com -bl old.example.com
```

Multiple names:

```
amass enum -d example.com -bl old.example.com,test.example.com
```

Useful when an engagement explicitly excludes particular hosts.

---

# 29. Blacklist File — `-blf`

Create:

```
blacklist.txt
```

Example:

```
old.example.com
test.example.com
internal.example.com
```

Then:

```
amass enum -d example.com -blf blacklist.txt
```

---

# 30. Include Specific Data Sources

List available sources:

```
amass enum -list
```

Then include selected sources:

```
amass enum -d example.com -include crtsh
```

Multiple:

```
amass enum -d example.com -include crtsh,certspotter
```

OWASP documents `-include` and `-exclude` for controlling data-source selection. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 31. Exclude Data Sources

Example:

```
amass enum -d example.com -exclude crtsh
```

Multiple:

```
amass enum -d example.com -exclude crtsh,certspotter
```

This is useful when:

- A provider is unavailable
- You have API problems
- You don't want to use a particular source
- You're troubleshooting enumeration

---

# 32. Include Source File — `-if`

Create:

```
sources.txt
```

Then:

```
amass enum -d example.com -if sources.txt
```

The file specifies sources to include.

---

# 33. Exclude Source File — `-ef`

```
amass enum -d example.com -ef exclude.txt
```

This is useful for reusable engagement configurations.

---

# 34. Include Unresolvable Names

Normally you may focus on names that resolve.

You can also request discovered DNS names that did not resolve:

```
amass enum -include-unresolvable -d example.com
```

OWASP documents this option for outputting DNS names that did not resolve. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

This can be valuable because an unresolved hostname can still be an important OSINT finding.

---

# 35. Data Operations Output — `-do`

Amass can write data-operation information:

```
amass enum -d example.com -do data.json
```

This is useful when you want to preserve structured enumeration data for later processing/import.

---

# 36. Graph Database

One of Amass's major differences from simpler tools is that it maintains a graph database.

Conceptually:

```
                example.com
                     │
         ┌───────────┼───────────┐
         ▼           ▼           ▼
       api         mail          dev
         │           │            │
         ▼           ▼            ▼
       IP-1        IP-2          IP-3
         │
         ▼
      network
```

Amass can retain relationships between:

- Domains
- Subdomains
- IP addresses
- Autonomous systems
- Networks
- Data sources
- DNS information

The OWASP guide describes the graph database as the persistent store for enumeration results. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 37. `db` — Database Management

List stored enumerations:

```
amass db -list
```

Show stored results:

```
amass db -show
```

For a particular domain:

```
amass db -show -d example.com
```

Show IPs:

```
amass db -show -ip -d example.com
```

Show IPv4:

```
amass db -show -ipv4 -d example.com
```

Show IPv6:

```
amass db -show -ipv6 -d example.com
```

Show sources:

```
amass db -show -src -d example.com
```

These database operations are documented by OWASP. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 38. Enumeration IDs

List stored enumerations:

```
amass db -list
```

You may see something conceptually like:

```
ID    Domain
1     example.com
2     example.org
```

Then:

```
amass db -show -enum 1
```

This lets you inspect a specific enumeration.

---

# 39. Import Data

Amass can import a data-operations JSON file:

```
amass db -import data.json
```

This is useful for preserving or moving investigation data.

---

# 40. `viz` — Visualization

Amass can create visualizations of the collected graph.

For example:

```
amass viz -d3 -d example.com
```

OWASP documents D3.js visualization output through `viz -d3`. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

The idea is:

```
Domains
   │
   ├── Subdomains
   │
   ├── IPs
   │
   ├── Networks
   │
   └── Relationships
          ↓
       Graph view
```

This becomes especially useful on larger engagements.

---

# 41. Visualize a Specific Enumeration

If the database contains multiple enumerations:

```
amass viz -enum 1 -d3
```

This uses enumeration ID `1`.

---

# 42. `intel` — Organization Intelligence

`intel` is different from `enum`.

Use:

```
amass intel -d example.com
```

Its purpose is broader organizational intelligence.

It can help identify:

- Additional domains
- Related infrastructure
- ASNs
- CIDRs
- Organization relationships
- Reverse-WHOIS-related information

OWASP describes `intel` as a way to discover additional root domains associated with the organization. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 43. Reverse WHOIS — `-whois`

Example:

```
amass intel -whois -d example.com
```

Conceptually:

```
Known domain
     ↓
registration intelligence
     ↓
related domains
```

This is particularly useful when an organization owns multiple domains.

---

# 44. ASN Intelligence — `-asn`

If you know an ASN:

```
amass intel -asn 13374
```

Multiple:

```
amass intel -asn 13374,14618
```

This can help identify domains/infrastructure associated with an ASN.

---

# 45. CIDR Intelligence — `-cidr`

Example:

```
amass intel -cidr 192.0.2.0/24
```

Multiple:

```
amass intel -cidr 192.0.2.0/24,198.51.100.0/24
```

This is useful when you already know network ranges associated with the organization.

---

# 46. IP Range — `-addr`

You can provide an IP range:

```
amass intel -addr 192.0.2.1-64
```

The documented syntax supports ranges such as:

```
192.168.1.1-254
```

and multiple values separated by commas. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 47. Organization Search — `-org`

Example:

```
amass intel -org "Example Corporation"
```

This searches AS-description information for the provided organization string. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 48. `intel` + IP Addresses

```
amass intel -ip -whois -d example.com
```

This combines:

```
WHOIS intelligence
+
IP output
```

IPv4 only:

```
amass intel -ipv4 -whois -d example.com
```

IPv6:

```
amass intel -ipv6 -whois -d example.com
```

---

# 49. Source Discovery in `intel`

```
amass intel -list
```

This lists available intelligence sources.

You can then select:

```
amass intel -include SOURCE -d example.com
```

or exclude:

```
amass intel -exclude SOURCE -d example.com
```

---

# 50. Configuration File

Amass supports configuration files:

```
amass enum -config config.ini -d example.com
```

or:

```
amass intel -config config.ini -d example.com
```

The configuration can control data sources and API credentials.

Rather than manually guessing configuration syntax, inspect the configuration examples shipped with your installed Amass version and its documentation.

---

# 51. API Keys

Amass can use external data sources requiring API credentials.

The important concept is:

```
Amass
  ↓
Data source
  ↓
API
  ↓
Additional OSINT
```

API sources can substantially increase discovery coverage.

However:

```
No API key
    ≠
Amass doesn't work
```

You can still use sources that don't require credentials.

---

# 52. Docker

OWASP documents Docker usage.

A typical pattern is:

```
docker run -v OUTPUT_DIR_PATH:/.config/amass/ \
    amass enum -d example.com
```

The mounted directory allows the graph database and output files to persist outside the container. [GitHub](https://github.com/owasp-amass/amass/wiki/Installation-Guide?utm_source=chatgpt.com)

---

# 53. A Good Beginner Workflow

For your learning, I recommend this progression.

### Step 1 — Basic

```
amass enum -d example.com
```

### Step 2 — Passive

```
amass enum -passive -d example.com
```

### Step 3 — Show sources

```
amass enum -passive -src -d example.com
```

### Step 4 — Show IPs

```
amass enum -passive -src -ip -d example.com
```

### Step 5 — Save

```
amass enum -passive -d example.com -o amass.txt
```

### Step 6 — JSON

```
amass enum -passive -d example.com -json amass.json
```

### Step 7 — Brute force

Only in scope:

```
amass enum -brute -w wordlist.txt -d example.com
```

### Step 8 — Active

Only when authorized:

```
amass enum -active -d example.com -p 80,443
```

---

# 54. Amass + theHarvester

Since you just learned theHarvester, these tools work well together.

Start:

```
theHarvester -d example.com -b crtsh,certspotter -f harvester
```

Then:

```
amass enum -passive -d example.com
```

You can also feed known names into Amass:

```
amass enum -d example.com -nf known.txt
```

Conceptually:

```
theHarvester
     │
     ▼
Public OSINT
     │
     ▼
known subdomains
     │
     ▼
Amass
     │
     ▼
additional DNS/OSINT enumeration
```

---

# 55. Amass + DNS Tools

Once Amass discovers:

```
api.example.com
```

use:

```
host api.example.com
```

Then:

```
nslookup api.example.com
```

Then for detailed analysis:

```
dig api.example.com
```

If it resolves to:

```
203.0.113.10
```

pivot:

```
whois 203.0.113.10
```

and:

```
dig -x 203.0.113.10
```

Your reconnaissance chain becomes:

```
Amass
  ↓
Subdomain
  ↓
host / nslookup
  ↓
IP
  ↓
dig
  ↓
DNS details
  ↓
whois
  ↓
Network ownership
```

---

# 56. Amass Brute Force vs Passive Discovery

This distinction is important.

### Passive

```
amass enum -passive -d example.com
```

Uses information already available through data sources.

### Brute force

```
amass enum -brute -d example.com
```

Actively generates DNS queries for candidate names.

For example:

```
admin.example.com
dev.example.com
vpn.example.com
api.example.com
```

So:

```
Passive
  ↓
"What has already been observed?"

Brute force
  ↓
"Does this candidate hostname exist?"
```

---

# 57. Active Mode

```
amass enum -active -d example.com
```

You can specify ports:

```
amass enum -active -d example.com -p 80,443,8080
```

This can involve active interaction with discovered infrastructure. OWASP's documentation describes active mode as reaching out to discovered assets and performing additional techniques such as certificate acquisition, DNS zone-transfer attempts, NSEC walking, and web crawling. [GitHub](https://github.com/JohnEarle/amass-develop/blob/master/doc/user_guide.md?utm_source=chatgpt.com)

Therefore:

```
-passive
```

and:

```
-active
```

should be treated very differently during an engagement.

---

# 58. Zone Transfer

Amass active enumeration can attempt DNS zone-transfer techniques.

You don't need to manually run the transfer just to understand the concept:

```
Authoritative DNS
       ↓
AXFR
       ↓
Potential zone records
```

You already learned the manual equivalent with `dig`:

```
dig @ns1.example.com example.com AXFR
```

Amass can incorporate such DNS enumeration into its active workflow. [GitHub](https://github.com/JohnEarle/amass-develop/blob/master/doc/user_guide.md?utm_source=chatgpt.com)

---

# 59. NSEC Walking

DNSSEC-related NSEC records can sometimes reveal additional names.

Conceptually:

```
DNSSEC
  ↓
NSEC
  ↓
name relationships
  ↓
possible hostname discovery
```

Amass's active enumeration can use NSEC walking as part of its broader active discovery process. [GitHub](https://github.com/JohnEarle/amass-develop/blob/master/doc/user_guide.md?utm_source=chatgpt.com)

---

# 60. Output Filtering

For a large output, you can use normal Linux tools.

Only subdomains:

```
amass enum -passive -d example.com | sort -u
```

Save unique results:

```
amass enum -passive -d example.com | sort -u > unique.txt
```

Count results:

```
amass enum -passive -d example.com | sort -u | wc -l
```

Search a particular hostname:

```
amass enum -passive -d example.com | grep -i api
```

---

# 61. Feed Amass Results into Other Tools

For example:

```
amass enum -passive -d example.com -o subdomains.txt
```

Then inspect each:

```
while read host; do
    echo "===== $host ====="
    host "$host"
done < subdomains.txt
```

Then potentially:

```
while read host; do
    dig "$host" A +short
done < subdomains.txt
```

This is a very useful beginner automation pattern.

---

# 62. Professional Recon Pipeline

A practical authorized external-recon workflow can look like:

```
                         TARGET
                            │
                            ▼
                         Amass
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
          Passive         Intel         Active
             │              │              │
             ▼              ▼              ▼
       Subdomains       Domains/ASN     DNS/network
             │
             ▼
       ┌─────┴─────┐
       ▼           ▼
     host        dig
       │           │
       └─────┬─────┘
             ▼
             IP
             │
       ┌─────┴─────┐
       ▼           ▼
     whois      reverse DNS
```

This is where Amass becomes much more powerful than using each DNS tool independently.

---

# 63. Important Options — Quick Reference

|Option|Purpose|Example|
|---|---|---|
|`-d`|Target domain(s)|`amass enum -d example.com`|
|`-df`|Domain file|`amass enum -df domains.txt`|
|`-passive`|Passive enumeration|`amass enum -passive -d example.com`|
|`-active`|Active enumeration|`amass enum -active -d example.com`|
|`-ip`|Show IP addresses|`amass enum -ip -d example.com`|
|`-ipv4`|Show IPv4|`amass enum -ipv4 -d example.com`|
|`-ipv6`|Show IPv6|`amass enum -ipv6 -d example.com`|
|`-src`|Show data sources|`amass enum -src -d example.com`|
|`-brute`|DNS brute force|`amass enum -brute -d example.com`|
|`-w`|Brute-force wordlist|`amass enum -brute -w words.txt -d example.com`|
|`-norecursive`|Disable recursive brute force|`amass enum -brute -norecursive -d example.com`|
|`-nf`|Known names file|`amass enum -nf names.txt -d example.com`|
|`-bl`|Blacklist names|`amass enum -bl old.example.com -d example.com`|
|`-blf`|Blacklist file|`amass enum -blf blacklist.txt -d example.com`|
|`-include`|Include data source(s)|`amass enum -include crtsh -d example.com`|
|`-exclude`|Exclude data source(s)|`amass enum -exclude crtsh -d example.com`|
|`-r`|Preferred DNS resolver|`amass enum -r 8.8.8.8 -d example.com`|
|`-rf`|Resolver file|`amass enum -rf resolvers.txt -d example.com`|
|`-o`|Text output|`amass enum -o results.txt -d example.com`|
|`-json`|JSON output|`amass enum -json results.json -d example.com`|
|`-oA`|Output prefix|`amass enum -oA scan -d example.com`|
|`-timeout`|Runtime in minutes|`amass enum -timeout 30 -d example.com`|
|`-max-dns-queries`|DNS concurrency|`amass enum -max-dns-queries 100 -d example.com`|
|`-include-unresolvable`|Include unresolved names|`amass enum -include-unresolvable -d example.com`|
|`-config`|Configuration file|`amass enum -config config.ini -d example.com`|
|`-list`|List data sources|`amass enum -list`|

---

# 64. `intel` Options Worth Knowing

|Option|Purpose|
|---|---|
|`-d`|Domain|
|`-df`|Domain file|
|`-whois`|Reverse-WHOIS intelligence|
|`-asn`|ASN intelligence|
|`-cidr`|CIDR intelligence|
|`-addr`|IP/range intelligence|
|`-org`|Organization search|
|`-active`|Active intelligence|
|`-ip`|Show IPs|
|`-ipv4`|Show IPv4|
|`-ipv6`|Show IPv6|
|`-src`|Show sources|
|`-r`|Preferred resolvers|
|`-o`|Text output|
|`-list`|List sources|

These are documented in OWASP's user guide. [GitHub](https://github.com/owasp-amass/amass/wiki/User-Guide?utm_source=chatgpt.com)

---

# 65. Commands You Should Memorize First

### Basic

```
amass enum -d example.com
```

### Passive

```
amass enum -passive -d example.com
```

### Sources

```
amass enum -passive -src -d example.com
```

### IPs

```
amass enum -passive -ip -d example.com
```

### IPv4

```
amass enum -ipv4 -d example.com
```

### IPv6

```
amass enum -ipv6 -d example.com
```

### Save

```
amass enum -passive -d example.com -o amass.txt
```

### JSON

```
amass enum -passive -d example.com -json amass.json
```

### Brute force

```
amass enum -brute -w wordlist.txt -d example.com
```

### Known names

```
amass enum -nf names.txt -d example.com
```

### Active

```
amass enum -active -d example.com -p 80,443
```

### Organization intelligence

```
amass intel -d example.com
```

### Reverse WHOIS

```
amass intel -whois -d example.com
```

### ASN

```
amass intel -asn 13374
```

### Database

```
amass db -list
```

```
amass db -show -d example.com
```

### Visualization

```
amass viz -d3 -d example.com
```

---

# 66. The Most Important Difference: Amass vs theHarvester

You just learned theHarvester, so this distinction is important.

|Feature|theHarvester|Amass|
|---|---|---|
|OSINT|✅|✅|
|Email discovery|Strong|Limited/not primary|
|Subdomain discovery|✅|⭐⭐⭐|
|DNS enumeration|Limited|⭐⭐⭐|
|DNS brute force|Limited/varies|✅|
|Active reconnaissance|Some capabilities|✅|
|ASN/CIDR intelligence|Limited|✅|
|Persistent graph database|❌|✅|
|Visualization|❌|✅|
|Enumeration tracking|❌|✅|
|DNS-focused workflow|Moderate|Excellent|

Think:

```
theHarvester
    ↓
OSINT aggregation

Amass
    ↓
Attack-surface mapping
    +
DNS enumeration
    +
Infrastructure relationships
    +
Persistent investigation database
```

OWASP specifically describes Amass as an attack-surface mapping and external asset-discovery tool. [GitHub](https://github.com/OWASP/DevGuide/blob/main/docs/en/06-verification/02-tools/02-amass.md?utm_source=chatgpt.com)