
---
**Subfinder** is a fast **passive subdomain enumeration** tool from ProjectDiscovery. It discovers subdomains of a target domain using multiple public sources such as certificate transparency, search engines, DNS datasets, and other passive intelligence providers.

> Use it only against domains you own or are explicitly authorized to assess.

---

## 1. What Subfinder is used for

Typical pentesting workflow:

```
Target domain
     │
     ▼
   Subfinder
     │
     ├── sub1.example.com
     ├── api.example.com
     ├── dev.example.com
     ├── mail.example.com
     └── staging.example.com
             │
             ▼
      DNS resolution
             │
             ▼
      httpx / nmap / nuclei
```

Subfinder is primarily for:

- Passive subdomain discovery
- Attack-surface enumeration
- Finding forgotten subdomains
- Discovering development/staging hosts
- Collecting subdomains from certificate transparency
- Combining multiple OSINT sources
- Feeding discovered hosts into other tools

---

# 2. Installation

### Kali Linux

```
sudo apt update
sudo apt install subfinder
```

Check:

```
subfinder -version
```

Help:

```
subfinder -h
```

If you install the latest ProjectDiscovery release manually:

```
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

Then make sure Go's binary directory is in your `PATH`.

---

# 3. Basic Syntax

```
subfinder [options] -d <domain>
```

Basic example:

```
subfinder -d example.com
```

Example output:

```
api.example.com
dev.example.com
mail.example.com
blog.example.com
staging.example.com
```

---

# 4. Most Important Options

|Option|Purpose|
|---|---|
|`-d`|Target domain|
|`-dL`|Read domains from a file|
|`-o`|Save output|
|`-silent`|Show only discovered subdomains|
|`-v`|Verbose output|
|`-all`|Use all available sources|
|`-s`|Specify sources|
|`-ls`|List available sources|
|`-recursive`|Find subdomains recursively|
|`-nW`|Remove wildcard results|
|`-oJ`|JSON output|
|`-oD`|Directory output|
|`-cs`|Show sources for each result|
|`-rl`|Requests per second|
|`-t`|Number of concurrent threads|
|`-timeout`|DNS timeout|
|`-max-time`|Maximum enumeration time|
|`-config`|Configuration file|
|`-pc`|Provider configuration file|

---

# 5. Enumerate One Domain

The command you'll use most:

```
subfinder -d example.com
```

For example, in an authorized lab:

```
subfinder -d test.example.com
```

---

# 6. Save Results

Use `-o`:

```
subfinder -d example.com -o subdomains.txt
```

Then:

```
cat subdomains.txt
```

Example:

```
api.example.com
dev.example.com
mail.example.com
portal.example.com
staging.example.com
```

---

# 7. Silent Mode

Normally Subfinder can display status information.

Use:

```
subfinder -d example.com -silent
```

This is particularly useful when piping output into another tool.

Example:

```
subfinder -d example.com -silent | httpx
```

Conceptually:

```
Subfinder
   ↓
subdomains only
   ↓
httpx
   ↓
live HTTP services
```

---

# 8. Verbose Mode

```
subfinder -d example.com -v
```

Useful when troubleshooting or understanding what Subfinder is doing.

---

# 9. List Available Sources

```
subfinder -ls
```

This shows the data sources supported by your installed version.

This is useful because available sources can change between versions.

---

# 10. Use Specific Sources

You can specify sources with `-s`.

Example:

```
subfinder -d example.com -s crtsh
```

Multiple sources:

```
subfinder -d example.com -s crtsh,hackertarget,rapiddns
```

The exact source names available on your installation should be checked with:

```
subfinder -ls
```

---

# 11. Use All Sources

```
subfinder -d example.com -all
```

This tells Subfinder to use all available sources rather than only the default source set.

Useful when you want maximum passive coverage.

---

# 12. Show Which Sources Found a Subdomain

Use:

```
subfinder -d example.com -cs
```

`-cs` means **show sources**.

Example conceptually:

```
api.example.com     [crtsh,hackertarget]
dev.example.com     [crtsh,waybackarchive]
mail.example.com    [securitytrails]
```

This can help determine where a particular result originated.

---

# 13. Multiple Domains

Create a file:

```
nano domains.txt
```

Example:

```
example.com
example.org
example.net
```

Run:

```
subfinder -dL domains.txt
```

Save:

```
subfinder -dL domains.txt -o all-subdomains.txt
```

Silent:

```
subfinder -dL domains.txt -silent
```

---

# 14. Multiple Options Together

A realistic command:

```
subfinder -d example.com -all -silent -o subdomains.txt
```

Breakdown:

```
-d example.com
    ↓
target

-all
    ↓
use all available sources

-silent
    ↓
only print results

-o subdomains.txt
    ↓
save results
```

Another example:

```
subfinder -d example.com -all -cs -o results.txt
```

Here:

```
-d       → target
-all     → all sources
-cs      → show source information
-o       → save results
```

---

# 15. Recursive Enumeration

Subfinder supports recursive enumeration:

```
subfinder -d example.com -recursive
```

For example, you might discover:

```
dev.example.com
```

and additional levels such as:

```
api.dev.example.com
test.api.dev.example.com
```

depending on available sources and data.

Recursive discovery can increase enumeration time and result volume.

---

# 16. Remove Wildcard Results

Use:

```
subfinder -d example.com -nW
```

This helps reduce wildcard-related false positives.

Wildcard DNS means something like:

```
anything.example.com
random.example.com
abc123.example.com
```

may all resolve because of a wildcard DNS record.

---

# 17. JSON Output

Use:

```
subfinder -d example.com -oJ results.json
```

This is useful when you want structured output for scripts or further processing.

Example:

```
subfinder -d example.com -oJ subdomains.json
```

---

# 18. Output Directory

Subfinder also supports directory-oriented output options in current versions.

Check:

```
subfinder -h
```

and look for:

```
-oD
```

For example:

```
subfinder -dL domains.txt -oD results/
```

This is particularly useful when enumerating many domains.

---

# 19. Rate Limiting

For controlling request rate:

```
subfinder -d example.com -rl 10
```

Meaning approximately:

```
10 requests/second
```

Useful when:

- APIs have rate limits
- You don't want excessive requests
- Running large enumeration jobs

---

# 20. Threads

You can control concurrency with:

```
subfinder -d example.com -t 20
```

Higher concurrency can increase speed but may increase load and rate-limit problems.

Example:

```
subfinder -d example.com -all -t 20 -o results.txt
```

---

# 21. Timeout

You can control DNS timeout behavior with:

```
subfinder -d example.com -timeout 10
```

For example:

```
subfinder -d example.com -timeout 20 -o results.txt
```

Useful when DNS responses are slow.

---

# 22. Maximum Enumeration Time

You can limit the total runtime:

```
subfinder -d example.com -max-time 10
```

This is useful when running automated reconnaissance pipelines.

---

# 23. Provider Configuration

Some Subfinder sources require API keys.

The provider configuration is generally stored under the Subfinder configuration directory.

You can locate the configuration path with:

```
subfinder -h
```

Look for:

```
-pc
```

which specifies the provider configuration file.

Typical workflow:

```
subfinder -d example.com
```

If a source requires an API key, configure it in the provider configuration file and rerun enumeration.

The exact available providers and configuration fields can change between releases, so use:

```
subfinder -ls
```

and the installed version's configuration.

---

# 24. Why API Keys Matter

Without API keys, Subfinder can still perform useful passive enumeration.

With configured providers, coverage can increase significantly.

Conceptually:

```
No API keys
     ↓
Free/public sources
     ↓
Some subdomains


API-enabled
     ↓
More intelligence providers
     ↓
Potentially greater coverage
```

Do not assume that an API-enabled scan finds every subdomain.

---

# 25. Important Sources Conceptually

Subfinder can aggregate information from sources such as:

```
Certificate Transparency
Search engines
DNS databases
Threat-intelligence services
Passive DNS
Internet-wide datasets
URL intelligence
Security platforms
```

The exact source list depends on the current Subfinder release and configuration.

Check:

```
subfinder -ls
```

---

# 26. Certificate Transparency Recon

Certificate Transparency is particularly useful for discovering hostnames that appear in TLS certificates.

For example:

```
example.com
api.example.com
dev.example.com
vpn.example.com
mail.example.com
```

Subfinder can automatically consume CT-related sources.

This is one reason Subfinder is useful even when a DNS brute-force scan is not being performed.

---

# 27. Subfinder Does NOT Mean "Find Every Subdomain"

This is important.

Suppose the real infrastructure contains:

```
api.example.com
dev.example.com
internal.example.com
vpn.example.com
```

Subfinder might return:

```
api.example.com
dev.example.com
vpn.example.com
```

but miss:

```
internal.example.com
```

because there may be no publicly indexed evidence for it.

Therefore:

```
Passive enumeration ≠ complete enumeration
```

Professional reconnaissance normally combines multiple techniques.

---

# 28. Subfinder + DNS Resolution

Subfinder discovers names.

You can then resolve them.

For example:

```
subfinder -d example.com -silent | dnsx
```

Conceptually:

```
Subfinder
    ↓
api.example.com
dev.example.com
vpn.example.com
    ↓
dnsx
    ↓
IP addresses
```

Save the subdomains first:

```
subfinder -d example.com -silent -o subdomains.txt
```

Then:

```
cat subdomains.txt | dnsx
```

---

# 29. Subfinder + httpx

One of the most useful combinations:

```
subfinder -d example.com -silent | httpx
```

This answers:

> Which discovered subdomains actually expose HTTP/HTTPS services?

Save first:

```
subfinder -d example.com -silent -o subdomains.txt
```

Then:

```
cat subdomains.txt | httpx -o live-hosts.txt
```

Pipeline:

```
                    ┌── Subfinder
                    │
example.com ────────┤
                    ▼
             subdomains.txt
                    │
                    ▼
                  httpx
                    │
                    ▼
             live web hosts
```

---

# 30. Subfinder + Nmap

First discover subdomains:

```
subfinder -d example.com -silent -o subdomains.txt
```

Resolve them:

```
cat subdomains.txt | dnsx -resp-only -o ips.txt
```

Then perform authorized service enumeration:

```
nmap -iL ips.txt
```

For a lab target, you could continue with:

```
nmap -sV -iL ips.txt
```

This separates:

```
Discovery
    ↓
Resolution
    ↓
Service enumeration
```

which is cleaner than blindly scanning everything.

---

# 31. Subfinder + Nuclei

For an authorized assessment:

```
subfinder -d example.com -silent | httpx -silent | nuclei
```

Pipeline:

```
example.com
     ↓
subfinder
     ↓
subdomains
     ↓
httpx
     ↓
HTTP services
     ↓
nuclei
     ↓
template-based security checks
```

For production engagements, scope and template selection should be controlled carefully.

---

# 32. Subfinder + Other Passive Recon

A strong passive workflow can look like:

```
subfinder -d example.com -silent -o subfinder.txt
```

Then combine with another passive source:

```
cat subfinder.txt other-results.txt | sort -u > all-subdomains.txt
```

Then:

```
cat all-subdomains.txt | dnsx
```

Then:

```
cat all-subdomains.txt | httpx
```

This is more effective than relying on a single source.

---

# 33. Remove Duplicate Results

When combining tools:

```
cat subfinder.txt other.txt | sort -u > unique-subdomains.txt
```

`sort -u` means:

```
sort
  +
unique
```

Example input:

```
api.example.com
dev.example.com
api.example.com
mail.example.com
dev.example.com
```

Output:

```
api.example.com
dev.example.com
mail.example.com
```

---

# 34. Practical Professional Workflow

For an authorized external assessment:

### Step 1 — Start passive enumeration

```
subfinder -d example.com -silent -o subdomains.txt
```

### Step 2 — Increase source coverage

```
subfinder -d example.com -all -silent -o subdomains-all.txt
```

### Step 3 — Deduplicate

```
sort -u subdomains-all.txt > unique-subdomains.txt
```

### Step 4 — Resolve DNS

```
cat unique-subdomains.txt | dnsx -silent -o resolved.txt
```

### Step 5 — Find HTTP services

```
cat unique-subdomains.txt | httpx -silent -o live-web.txt
```

### Step 6 — Continue with authorized testing

```
Subdomains
    ↓
DNS
    ↓
IP addresses
    ↓
HTTP services
    ↓
Technology identification
    ↓
Vulnerability assessment
```

---

# 35. Useful One-Liners

### Basic

```
subfinder -d example.com
```

### Quiet output

```
subfinder -d example.com -silent
```

### Save results

```
subfinder -d example.com -silent -o subdomains.txt
```

### All sources

```
subfinder -d example.com -all -silent
```

### Recursive

```
subfinder -d example.com -recursive -silent
```

### Show sources

```
subfinder -d example.com -cs
```

### Specific sources

```
subfinder -d example.com -s crtsh,hackertarget
```

### Multiple domains

```
subfinder -dL domains.txt -silent
```

### JSON

```
subfinder -d example.com -oJ results.json
```

### Rate limiting

```
subfinder -d example.com -rl 10
```

### Controlled concurrency

```
subfinder -d example.com -t 20
```

### Subfinder → httpx

```
subfinder -d example.com -silent | httpx -silent
```

### Subfinder → DNS resolution

```
subfinder -d example.com -silent | dnsx -silent
```

---

# 36. Common Mistakes

### Mistake 1 — Assuming Subfinder is active scanning

Subfinder is primarily a **passive enumeration** tool.

It does not replace:

```
Nmap
DNS brute forcing
Port scanning
Web crawling
Vulnerability scanning
```

---

### Mistake 2 — Using only one source

Don't assume:

```
subfinder -d example.com
```

represents the complete attack surface.

For broader passive coverage:

```
subfinder -d example.com -all
```

---

### Mistake 3 — Not resolving results

Finding:

```
dev.example.com
```

doesn't tell you whether it currently resolves.

Use DNS resolution afterward:

```
cat subdomains.txt | dnsx
```

---

### Mistake 4 — Not checking HTTP availability

A subdomain may exist but not host a web application.

Use:

```
cat subdomains.txt | httpx
```

---

### Mistake 5 — Forgetting deduplication

When combining sources:

```
sort -u results.txt
```

---

### Mistake 6 — Blindly increasing threads

This:

```
-t 1000
```

isn't automatically better.

High concurrency can cause:

- Rate limiting
- API exhaustion
- DNS failures
- Unnecessary load

Use sensible values.

---

# 37. Subfinder vs Amass vs theHarvester

|Tool|Main Strength|
|---|---|
|**Subfinder**|Fast passive subdomain discovery|
|**Amass**|Deep attack-surface mapping and DNS intelligence|
|**theHarvester**|Broad OSINT collection|
|**dnsx**|DNS resolution|
|**httpx**|HTTP service probing|
|**Nmap**|Port/service enumeration|

A useful mental model:

```
Google Dorks
     ↓
WHOIS
     ↓
theHarvester
     ↓
Amass / Subfinder
     ↓
DNS resolution
     ↓
HTTP probing
     ↓
Port scanning
     ↓
Vulnerability assessment
```

---

# 38. Commands You Should Memorize

If you're preparing for a pentesting interview, memorize these first:

```
# Basic
subfinder -d example.com

# Silent
subfinder -d example.com -silent

# Save
subfinder -d example.com -silent -o subdomains.txt

# All sources
subfinder -d example.com -all -silent

# Multiple domains
subfinder -dL domains.txt -silent

# Recursive
subfinder -d example.com -recursive

# Show sources
subfinder -d example.com -cs

# List sources
subfinder -ls

# JSON
subfinder -d example.com -oJ results.json

# Pipeline
subfinder -d example.com -silent | httpx -silent

# DNS resolution
subfinder -d example.com -silent | dnsx -silent
```

### The key concept

Remember:

> **Subfinder = passive subdomain discovery.**

And in a professional recon pipeline:

```
SUBFINDER
   │
   ▼
SUBDOMAINS
   │
   ├──────────────► DNSX ──────► IPs
   │
   └──────────────► HTTPX ─────► Live Web Services
                                  │
                                  ▼
                               NUCLEI
```