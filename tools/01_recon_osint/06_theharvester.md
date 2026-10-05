
---
[theHarvester official repository](https://github.com/laramies/theHarvester?utm_source=chatgpt.com)

`theHarvester` is an **OSINT / passive reconnaissance tool** used to gather publicly available information about a domain or organization.

It can collect things such as:

- Subdomains / hostnames
- Email addresses
- IP addresses
- URLs
- ASNs
- People
- Breach-related information
- Certificate-transparency data
- Information from search engines and public datasets

The current project supports multiple discovery providers and capability selectors. Some providers require API keys, while others can work without credentials. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

For pentesting, use it only against domains/organizations that are **within your authorized scope**.

---

# 1. Installation on Kali

Kali packages theHarvester directly:

```
sudo apt update
sudo apt install theharvester
```

Verify:

```
theHarvester -h
```

Check the installed version:

```
theHarvester --version
```

The current project documentation recommends checking `theHarvester -h` because available options and sources can change between releases. [GitHub](https://github.com/allingeek/theharvester/blob/master/docs/wiki/Installation.md?utm_source=chatgpt.com)

---

# 2. Basic Syntax

The fundamental syntax is:

```
theHarvester -d DOMAIN -b SOURCE
```

For example:

```
theHarvester -d example.com -b crtsh
```

Breakdown:

```
theHarvester
     │
     ├── -d example.com
     │       └── target domain
     │
     └── -b crtsh
             └── discovery source
```

A basic passive query can use multiple sources:

```
theHarvester -d example.com -b crtsh,certspotter
```

The current project documentation uses `example.com` for syntax examples and specifically demonstrates `crtsh` and `certspotter` as passive certificate sources. [GitHub](https://github.com/reeyarn/theharvester/blob/master/docs/wiki/Quick-Start.md?utm_source=chatgpt.com)

---

# 3. First Command to Run

Always start with:

```
theHarvester -h
```

This displays the options supported by **your installed version**.

This matters because theHarvester's source catalog and CLI capabilities have evolved substantially across releases. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 4. Basic Domain Enumeration

```
theHarvester -d example.com -b crtsh
```

You can also use:

```
theHarvester -d example.com -b certspotter
```

Or:

```
theHarvester -d example.com -b crtsh,certspotter
```

Think of:

```
-d
 ↓
domain

-b
 ↓
source(s)
```

---

# 5. `-d` — Domain

`-d` specifies the target domain.

Syntax:

```
theHarvester -d DOMAIN
```

Example:

```
theHarvester -d example.com -b crtsh
```

For another authorized target:

```
theHarvester -d company.example -b crtsh
```

Do not provide a full URL:

```
❌ https://example.com/login
```

Use:

```
✅ example.com
```

---

# 6. `-b` — Data Source

`-b` specifies which discovery source(s) to use.

Syntax:

```
theHarvester -d example.com -b SOURCE
```

Multiple sources:

```
theHarvester -d example.com -b crtsh,certspotter
```

The current version supports both explicit source names and capability selectors such as `subdomains`, `emails`, `ips`, `asns`, `urls`, `people`, and `breaches`. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 7. Using Multiple Sources

Example:

```
theHarvester -d example.com -b crtsh,certspotter,commoncrawl
```

Conceptually:

```
                  example.com
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        crtsh      certspotter   commoncrawl
          │            │            │
          └────────────┼────────────┘
                       ▼
                consolidated data
```

This is generally preferable to depending on one provider.

---

# 8. `-b all`

The current version supports:

```
theHarvester -d example.com -b all
```

This selects the catalogued **P0 passive sources**. It does not mean that every possible active operation is automatically performed; P1/P2 activity requires explicit selection. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

For learning, however, I recommend understanding individual sources first.

Why?

Because if:

```
theHarvester -d example.com -b all
```

produces an error, it becomes harder to determine which provider caused it.

---

# 9. Capability Selectors

Current theHarvester versions support capability selectors.

Examples:

```
theHarvester -d example.com -b subdomains
```

```
theHarvester -d example.com -b emails
```

```
theHarvester -d example.com -b ips
```

```
theHarvester -d example.com -b urls
```

```
theHarvester -d example.com -b asns
```

```
theHarvester -d example.com -b people
```

```
theHarvester -d example.com -b breaches
```

These select sources capable of returning that type of information. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 10. Subdomain Enumeration

One of the most important uses:

```
theHarvester -d example.com -b subdomains
```

You may discover:

```
www.example.com
mail.example.com
dev.example.com
api.example.com
vpn.example.com
```

The output depends entirely on what the selected public sources know.

An empty result **does not prove that no subdomains exist**.

---

# 11. Email Enumeration

```
theHarvester -d example.com -b emails
```

Potential output:

```
user@example.com
admin@example.com
support@example.com
```

This is useful for:

- OSINT
- Attack-surface documentation
- Identifying organizational naming conventions
- Authorized phishing-awareness assessments

An email appearing in public data does not necessarily mean it is currently active.

---

# 12. URL Discovery

```
theHarvester -d example.com -b urls
```

Potential findings might include:

```
https://example.com/
https://example.com/login
https://api.example.com/
```

Treat discovered URLs as **leads for further authorized validation**, not proof of a vulnerability.

---

# 13. IP Discovery

```
theHarvester -d example.com -b ips
```

Potential output:

```
203.0.113.10
203.0.113.20
```

You can then pivot:

```
whois 203.0.113.10
```

or:

```
host 203.0.113.10
```

or:

```
dig -x 203.0.113.10
```

This connects theHarvester to the other reconnaissance tools you've just learned.

---

# 14. ASN Discovery

```
theHarvester -d example.com -b asns
```

If ASNs are discovered, they can help understand the organization's network presence.

You can then investigate the ASN using appropriate network-recon tools.

---

# 15. People / Names

```
theHarvester -d example.com -b people
```

Depending on the provider, publicly associated names may be returned.

Treat these results carefully:

```
person found
     ≠
current employee
```

OSINT datasets can be stale or incorrectly attributed.

---

# 16. Breach-Related Sources

The current tool includes a `breaches` capability. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

Example:

```
theHarvester -d example.com -b breaches
```

Some breach-related providers require authentication and may only work for domains/accounts you are authorized to investigate. For example, the current documentation distinguishes public breach-catalogue querying from authenticated verified-domain HIBP access. [GitHub](https://github.com/laramies/theHarvester/blob/master/docs/wiki/Configuration-and-API-Keys.md?utm_source=chatgpt.com)

---

# 17. Certificate Transparency — `crtsh`

Certificate Transparency is particularly useful for discovering hostnames that have appeared in certificates.

```
theHarvester -d example.com -b crtsh
```

Conceptually:

```
example.com
     ↓
Certificate Transparency
     ↓
certificates
     ↓
hostnames
     ↓
potential subdomains
```

For example, certificates may reveal names such as:

```
www.example.com
api.example.com
dev.example.com
mail.example.com
```

---

# 18. CertSpotter

Another certificate-related source:

```
theHarvester -d example.com -b certspotter
```

Combine:

```
theHarvester -d example.com -b crtsh,certspotter
```

This gives you two independent certificate-data sources.

---

# 19. Common Crawl

If available in your installed source catalog:

```
theHarvester -d example.com -b commoncrawl
```

Historical/public web-crawl information can reveal URLs and hostnames that are not obvious from a current website.

---

# 20. URLScan

The current source catalog includes `urlscan`, which can provide subdomains, IPs, ASNs, and URLs. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

Example:

```
theHarvester -d example.com -b urlscan
```

This can be particularly useful for discovering infrastructure observed in public scans.

---

# 21. VirusTotal

Where configured and available:

```
theHarvester -d example.com -b virustotal
```

The current source matrix identifies VirusTotal as an API-key source. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 22. Shodan

The current source catalog contains a Shodan discovery source, which requires a key, and separately supports Shodan host enrichment. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

For source-based discovery:

```
theHarvester -d example.com -b shodan
```

Depending on the version/configuration, you may also encounter the separate Shodan enrichment option discussed below.

---

# 23. `-s` / `--shodan`

The current version has separate Shodan host enrichment.

Check your exact syntax:

```
theHarvester -h | grep -i shodan
```

The project documentation distinguishes the Shodan source from `-s` / `--shodan` enrichment. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

This distinction is important:

```
-b shodan
    ↓
discovery source

-s / --shodan
    ↓
Shodan host enrichment
```

---

# 24. Result Limits — `-l`

TheHarvester can limit how many results/pages are collected.

Check:

```
theHarvester -h | grep -E -- "-l|limit"
```

In versions supporting the classic `-l` option:

```
theHarvester -d example.com -b crtsh -l 100
```

Conceptually:

```
-l 100
   ↓
limit collection to 100 results
```

The exact semantics can vary by source/version.

The current project also documents a shared:

```
--limit
```

option. `--limit 0` removes the shared per-source result cap, subject to provider quotas and runtime safeguards. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 25. `--limit`

Current versions:

```
theHarvester -d example.com -b crtsh --limit 100
```

Remove the local result cap:

```
theHarvester -d example.com -b crtsh --limit 0
```

However:

```
--limit 0
```

does **not** mean unlimited Internet access.

Provider quotas, rate limits, and safety/runtime limits can still stop collection. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 26. Save Results — `-f`

Save a report:

```
theHarvester -d example.com -b crtsh -f report
```

The current version writes:

```
report.jsonl
report.json
report.xml
```

The JSONL format is the primary automation/interchange format, while JSON/XML are compatibility reports. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 27. Why Saving Results Matters

Instead of:

```
theHarvester -d example.com -b crtsh
```

use:

```
theHarvester -d example.com -b crtsh -f example-recon
```

Then you have:

```
example-recon.jsonl
example-recon.json
example-recon.xml
```

You can preserve this as part of your assessment evidence.

---

# 28. JSONL

The current version treats JSONL as the primary machine-readable format.

```
theHarvester -d example.com -b crtsh -f report
```

You can inspect it with:

```
cat report.jsonl
```

or:

```
less report.jsonl
```

You can also process it with tools such as:

```
jq
```

For example:

```
jq . report.jsonl
```

---

# 29. `-r` — DNS Resolution

The current version supports DNS resolution with:

```
theHarvester -d example.com -b crtsh -r
```

This introduces additional DNS activity.

The official documentation explicitly distinguishes passive provider lookups from DNS resolution and recommends using `-r` only for authorized domains. [GitHub](https://github.com/reeyarn/theharvester/blob/master/docs/wiki/Quick-Start.md?utm_source=chatgpt.com)

Conceptually:

```
Passive source
     ↓
discover hostname
     ↓
-r
     ↓
DNS resolution
     ↓
IP address
```

---

# 30. Custom Resolver

You can provide resolver addresses or a resolver file.

Example:

```
theHarvester -d example.com -b crtsh -r 8.8.8.8
```

Or a resolver file:

```
8.8.8.8
1.1.1.1
9.9.9.9
```

Then:

```
theHarvester -d example.com -b crtsh -r resolvers.txt
```

The current documentation explicitly supports a resolver IP, comma-separated resolver IPs, or a resolver file. [GitHub](https://github.com/reeyarn/theharvester/blob/master/docs/wiki/Quick-Start.md?utm_source=chatgpt.com)

---

# 31. DNS Brute Force — `-c`

The current tool supports DNS brute-force activity.

Check the exact syntax on your version:

```
theHarvester -h | grep -E -- "-c|brute"
```

Conceptually:

```
wordlist
   ↓
www
mail
dev
vpn
api
admin
   ↓
DNS queries
   ↓
potential subdomains
```

Because this generates DNS queries, it is **not purely passive OSINT**.

Only perform it within your authorized scope.

---

# 32. Reverse DNS — `-n`

The current version also supports reverse-DNS activity.

Check:

```
theHarvester -h | grep -E -- "-n|reverse"
```

Conceptually:

```
discovered IP range
       ↓
reverse DNS
       ↓
hostnames
```

This is another example of why theHarvester should not always be thought of as a purely passive tool.

---

# 33. Recursive DNS

Current versions support recursive DNS functionality through an option such as:

```
--dns-recursive-depth
```

Check:

```
theHarvester -h | grep -i recursive
```

This controls DNS recursion behavior in versions that expose it. The current README classifies recursive DNS as P1 activity requiring explicit selection. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 34. Takeover Checks — `-t`

Current versions support takeover checks.

Check:

```
theHarvester -h | grep -E -- "-t|takeover"
```

Conceptually:

```
discovered subdomain
       ↓
takeover check
       ↓
possible dangling/external resource
```

Important:

A tool reporting a possible takeover condition is **not automatically proof of an exploitable takeover**. It should be manually validated within the engagement.

---

# 35. API Path Scanning — `-a`

Current versions also expose API-path scanning.

Check:

```
theHarvester -h | grep -E -- "-a|api"
```

This is active behavior and should only be used against authorized targets.

---

# 36. Screenshots

Current versions support screenshots:

```
--screenshot
```

Check:

```
theHarvester -h | grep -i screenshot
```

The documentation classifies screenshots as P2/direct activity. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

A screenshot can help visually identify:

- Login portals
- Web applications
- Default pages
- Development interfaces
- Different applications hosted across discovered subdomains

Screenshots can also contain sensitive information, so treat them as engagement artifacts.

---

# 37. Source Workers — `-j`

The current version supports controlling the number of source workers:

```
theHarvester -d example.com -b crtsh,certspotter -j 5
```

Conceptually:

```
-j 5
 ↓
run up to 5 source workers
```

The current documentation states that three discovery sources run concurrently by default and `-j` / `--source-workers` changes that worker count. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

Check your installation:

```
theHarvester -h | grep -E -- "-j|source-workers"
```

---

# 38. Proxies — `-p`

Current versions can use configured HTTP/SOCKS5 proxies.

First inspect:

```
cat ~/.theHarvester/proxies.yaml
```

The current configuration documentation describes:

```
http:
  - 127.0.0.1:8080

socks5:
  - 127.0.0.1:9050
```

Then enable configured proxy usage with:

```
theHarvester -d example.com -b crtsh -p
```

The current documentation explicitly warns that a proxy does **not** make an assessment anonymous or change its authorization boundary. [GitHub](https://github.com/laramies/theHarvester/blob/master/docs/wiki/Configuration-and-API-Keys.md?utm_source=chatgpt.com)

---

# 39. API Keys

Many sources require API credentials.

The current configuration file is typically:

```
~/.theHarvester/api-keys.yaml
```

The tool can also read system-level configuration from:

```
/etc/theHarvester/
```

or:

```
/usr/local/etc/theHarvester/
```

The current documentation recommends protecting the file:

````
chmod 600 ~/.theHarvester/api-keys.yaml
``` :chatgpt-content-reference{index="23"}


---

# 40. Configure API Keys

Open:

```bash
nano ~/.theHarvester/api-keys.yaml
````

The exact fields depend on the provider.

For example, the current documentation shows a Censys configuration structure resembling:

```
apikeys:
  censys:
    token: YOUR_TOKEN
    organization_id: YOUR_ORGANIZATION_ID
```

GitHub:

```
apikeys:
  github:
    key: YOUR_TOKEN
```

Tomba:

```
apikeys:
  tomba:
    key: YOUR_KEY
    secret: YOUR_SECRET
```

Use the exact schema generated by your installed version rather than copying an old configuration from an Internet tutorial. [GitHub](https://github.com/laramies/theHarvester/blob/master/docs/wiki/Configuration-and-API-Keys.md?utm_source=chatgpt.com)

---

# 41. API-Key Source Workflow

Suppose you have an authorized API key for a provider.

First:

```
theHarvester -h
```

Identify the source name.

Then configure the key:

```
nano ~/.theHarvester/api-keys.yaml
```

Then run:

```
theHarvester -d example.com -b SOURCE
```

If the provider requires a result limit:

```
theHarvester -d example.com -b SOURCE --limit 100
```

---

# 42. Why API Sources Sometimes Fail

You may see errors because of:

```
No API key
Invalid API key
Expired API key
Rate limit
Provider quota
Provider unavailable
Changed API
Network failure
```

Don't immediately conclude:

```
"theHarvester doesn't work."
```

Instead isolate the provider:

```
theHarvester -d example.com -b crtsh
```

Then:

```
theHarvester -d example.com -b another-source
```

This tells you which source is causing the issue.

---

# 43. A Good Beginner Command

Start with:

```
theHarvester -d example.com -b crtsh,certspotter
```

Then save:

```
theHarvester -d example.com -b crtsh,certspotter -f example-recon
```

Then add more passive sources:

```
theHarvester -d example.com -b crtsh,certspotter,commoncrawl
```

Then DNS resolution:

```
theHarvester -d example.com -b crtsh,certspotter -r
```

This gives you a gradual progression:

```
Passive
  ↓
Multiple passive sources
  ↓
Save evidence
  ↓
DNS resolution
  ↓
Active enumeration
```

---

# 44. Professional Recon Workflow

For an authorized domain, a useful workflow is:

### Phase 1 — Passive discovery

```
theHarvester -d example.com -b crtsh,certspotter,commoncrawl
```

### Phase 2 — Save

```
theHarvester -d example.com -b crtsh,certspotter,commoncrawl -f recon
```

### Phase 3 — Subdomain-focused

```
theHarvester -d example.com -b subdomains
```

### Phase 4 — Email-focused

```
theHarvester -d example.com -b emails
```

### Phase 5 — DNS resolution

```
theHarvester -d example.com -b crtsh,certspotter -r
```

### Phase 6 — Feed discoveries into DNS tools

```
host discovered.example.com
```

```
dig discovered.example.com
```

### Phase 7 — Investigate IPs

```
whois <IP>
```

```
dig -x <IP>
```

This is where your previous tools connect together.

---

# 45. Full Recon Chain

Think of your current toolkit as:

```
                    TARGET
                      │
                      ▼
                 theHarvester
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   Subdomains      Emails          URLs
        │
        ▼
      host
        │
        ▼
        IP
        │
   ┌────┴─────┐
   ▼          ▼
 whois       dig
   │          │
   │     ┌────┼────┐
   │     ▼    ▼    ▼
   │     A    MX   NS
   │
   ▼
Network /
Organization
```

This is a much more useful way to learn these tools than treating each command as an isolated utility.

---

# 46. Example End-to-End Lab

Use a domain you own or a deliberately authorized lab target.

### 1. Start passive

```
theHarvester -d example.com -b crtsh,certspotter
```

### 2. Save

```
theHarvester -d example.com -b crtsh,certspotter -f recon
```

### 3. Resolve discovered hosts

```
theHarvester -d example.com -b crtsh,certspotter -r
```

### 4. Investigate a discovered hostname

```
host api.example.com
```

### 5. Detailed DNS

```
dig api.example.com
```

### 6. Nameservers

```
host -t NS example.com
```

### 7. IP ownership

```
whois <discovered-ip>
```

### 8. Reverse DNS

```
host <discovered-ip>
```

or:

```
dig -x <discovered-ip>
```

---

# 47. Common Mistake: Using `-b all` Immediately

This:

```
theHarvester -d example.com -b all
```

may contact many providers, consume quotas, and make failures harder to diagnose.

The current project documentation explicitly recommends starting with a small source set and choosing sources deliberately. [GitHub](https://github.com/reeyarn/theharvester/blob/master/docs/wiki/Quick-Start.md?utm_source=chatgpt.com)

Better:

```
theHarvester -d example.com -b crtsh,certspotter
```

Then expand.

---

# 48. Common Mistake: Assuming One Source Is Complete

Suppose:

```
theHarvester -d example.com -b crtsh
```

finds:

```
api.example.com
```

but doesn't find:

```
dev.example.com
```

That doesn't prove `dev.example.com` doesn't exist.

Different sources have different visibility.

Use multiple sources:

```
theHarvester -d example.com -b crtsh,certspotter,commoncrawl
```

and corroborate with other reconnaissance techniques.

---

# 49. Common Mistake: Treating OSINT as Verified Truth

Suppose theHarvester returns:

```
admin@example.com
```

That means:

```
Public source associated this email with the target.
```

It does **not automatically mean**:

```
The account exists.
The person currently works there.
The password is valid.
The account is usable.
```

Similarly:

```
dev.example.com
```

means:

```
A source observed the hostname.
```

It does not automatically mean:

```
The server is currently online.
The hostname is in scope.
The application is vulnerable.
```

Always validate.

---

# 50. Important Options — Quick Reference

Because the exact CLI evolves, confirm with:

```
theHarvester -h
```

The important current concepts are:

|Option|Purpose|
|---|---|
|`-d`|Target domain|
|`-b`|Data source / capability|
|`-f`|Save report|
|`-l`|Source/result limit in versions supporting it|
|`--limit`|Current shared result limit|
|`-r`|DNS resolution|
|`-c`|DNS brute-force activity|
|`-n`|Reverse DNS|
|`-t`|Takeover checks|
|`-a`|API-path scanning|
|`-s` / `--shodan`|Shodan enrichment|
|`-p`|Use configured proxy|
|`-j` / `--source-workers`|Source concurrency|
|`--screenshot`|Screenshot discovered web targets|
|`--dns-recursive-depth`|DNS recursive behavior|

Some options are active rather than passive, so don't assume that every theHarvester invocation is harmless passive OSINT. The current project explicitly classifies DNS, takeover, HTTP/API, screenshots, and related functions separately from passive provider lookups. [GitHub](https://github.com/laramies/theHarvester/blob/master/README.md?plain=1&utm_source=chatgpt.com)

---

# 51. Commands to Memorize

### Help

```
theHarvester -h
```

### Basic passive

```
theHarvester -d example.com -b crtsh
```

### Multiple sources

```
theHarvester -d example.com -b crtsh,certspotter
```

### All passive sources

```
theHarvester -d example.com -b all
```

### Subdomains

```
theHarvester -d example.com -b subdomains
```

### Emails

```
theHarvester -d example.com -b emails
```

### URLs

```
theHarvester -d example.com -b urls
```

### IPs

```
theHarvester -d example.com -b ips
```

### ASNs

```
theHarvester -d example.com -b asns
```

### People

```
theHarvester -d example.com -b people
```

### Save report

```
theHarvester -d example.com -b crtsh -f report
```

### Resolve hosts

```
theHarvester -d example.com -b crtsh -r
```

### Custom resolver

```
theHarvester -d example.com -b crtsh -r 8.8.8.8
```

### Limit results

```
theHarvester -d example.com -b crtsh --limit 100
```

### No local result cap

```
theHarvester -d example.com -b crtsh --limit 0
```

### Proxy

```
theHarvester -d example.com -b crtsh -p
```

---

# 52. TheHarvester Mental Model

Don't memorize the tool as a collection of random flags.

Think:

```
                    theHarvester
                         │
                 -d example.com
                         │
                         ▼
                    Data Sources
                         │
       ┌─────────────────┼─────────────────┐
       ▼                 ▼                 ▼
   Search/OSINT       Certificates      Datasets
       │                 │                 │
       └─────────────────┼─────────────────┘
                         ▼
                  Normalized Results
                         │
       ┌─────────┬───────┼───────┬─────────┐
       ▼         ▼       ▼       ▼         ▼
   Subdomains  Emails    IPs    URLs      ASNs
       │
       ▼
   DNS resolution (-r)
       │
       ▼
     IPs
       │
       ├── whois
       ├── host
       └── dig
```

### The core commands I would memorize first

```
theHarvester -d example.com -b crtsh
```

```
theHarvester -d example.com -b crtsh,certspotter
```

```
theHarvester -d example.com -b subdomains
```

```
theHarvester -d example.com -b emails
```

```
theHarvester -d example.com -b crtsh -f recon
```

```
theHarvester -d example.com -b crtsh -r
```