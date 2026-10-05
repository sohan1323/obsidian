
---
[Official Assetfinder repository](https://github.com/tomnomnom/assetfinder?utm_source=chatgpt.com)

**Assetfinder** is a lightweight passive reconnaissance tool by **Tomnomnom** used to find domains and subdomains associated with a target domain. It queries several passive sources such as `crt.sh`, CertSpotter, HackerTarget, ThreatCrowd, Wayback Machine, BufferOver, VirusTotal, and others. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

It is intentionally much simpler than tools such as Amass or Subfinder.

> Use active enumeration and subsequent scanning only against systems you own or are authorized to test.

---

# 1. What Assetfinder Does

Suppose your authorized target is:

```
example.com
```

Assetfinder may discover:

```
api.example.com
dev.example.com
mail.example.com
vpn.example.com
blog.example.com
staging.example.com
```

Its basic workflow is:

```
Target domain
     │
     ▼
 Assetfinder
     │
     ├── crt.sh
     ├── CertSpotter
     ├── HackerTarget
     ├── Wayback Machine
     ├── ThreatCrowd
     ├── BufferOver
     ├── VirusTotal*
     └── other configured sources
     │
     ▼
Subdomains / related domains
```

Some sources require API credentials. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

---

# 2. Installation

## Using Go

Current upstream documentation provides:

```
go install github.com/tomnomnom/assetfinder@latest
```

Then verify:

```
assetfinder --help
```

If the binary isn't found, check:

```
go env GOPATH
```

Usually the binary will be under:

```
$(go env GOPATH)/bin/
```

Add it to your PATH if necessary:

```
export PATH="$PATH:$(go env GOPATH)/bin"
```

The upstream repository also documents downloadable releases for supported platforms. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

---

# 3. Basic Syntax

Assetfinder has a very small CLI:

```
assetfinder [--subs-only] <domain>
```

For example:

```
assetfinder example.com
```

That's essentially the entire core syntax.

---

# 4. Basic Enumeration

```
assetfinder example.com
```

Possible output:

```
example.com
api.example.com
dev.example.com
mail.example.com
blog.example.com
example.net
related.example.org
```

Notice something important:

**Without `--subs-only`, Assetfinder can return related domains in addition to subdomains.** [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

---

# 5. `--subs-only`

This is the most important option.

```
assetfinder --subs-only example.com
```

It restricts output to subdomains associated with the supplied domain.

Example:

```
api.example.com
dev.example.com
mail.example.com
vpn.example.com
```

Instead of potentially returning unrelated/related root domains.

### Memorize this:

```
assetfinder --subs-only example.com
```

For normal pentesting subdomain enumeration, this is usually the command you want.

---

# 6. Difference Between Normal and `--subs-only`

### Normal

```
assetfinder example.com
```

Potentially:

```
example.com
api.example.com
dev.example.com
some-related-domain.com
```

### Subdomains only

```
assetfinder --subs-only example.com
```

Output:

```
api.example.com
dev.example.com
mail.example.com
```

So:

```
assetfinder
      │
      ├── related domains
      └── subdomains

assetfinder --subs-only
      │
      └── subdomains
```

---

# 7. Save Results to a File

Assetfinder itself has a deliberately minimal interface and doesn't provide a dedicated `-o` output flag.

Use shell redirection:

```
assetfinder --subs-only example.com > subdomains.txt
```

Read it:

```
cat subdomains.txt
```

Count results:

```
wc -l subdomains.txt
```

---

# 8. Remove Duplicates

This is extremely useful when combining Assetfinder with other enumeration tools.

```
assetfinder --subs-only example.com | sort -u
```

Save:

```
assetfinder --subs-only example.com | sort -u > subdomains.txt
```

Why?

Input:

```
api.example.com
dev.example.com
api.example.com
mail.example.com
dev.example.com
```

After:

```
sort -u
```

you get:

```
api.example.com
dev.example.com
mail.example.com
```

---

# 9. Stdin / Piping

Assetfinder can also be incorporated into Unix pipelines.

For example:

```
echo "example.com" | assetfinder
```

This is useful when building reconnaissance pipelines.

You can also feed domains from another command:

```
cat domains.txt | assetfinder
```

This is particularly useful when chaining multiple tools.

---

# 10. Multiple Domains

Suppose:

```
domains.txt
```

contains:

```
example.com
example.org
example.net
```

You can use:

```
cat domains.txt | assetfinder
```

Then clean the output:

```
cat domains.txt | assetfinder | sort -u
```

Save:

```
cat domains.txt | assetfinder | sort -u > all-assets.txt
```

### Important

Assetfinder's upstream README documents its basic positional-domain syntax and `--subs-only`; its interface is intentionally minimal. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

---

# 11. Important Data Sources

The upstream repository currently lists these implemented sources:

|Source|Purpose|
|---|---|
|`crt.sh`|Certificate Transparency|
|CertSpotter|Certificate/subdomain discovery|
|HackerTarget|Passive DNS/domain intelligence|
|ThreatCrowd|Threat intelligence|
|Wayback Machine|Historical URLs/domains|
|BufferOver|DNS/passive data|
|Facebook|Requires app credentials|
|VirusTotal|Requires API key|
|FindSubdomains|Requires Spyse API token|

Some sources therefore work immediately while others require configuration.

---

# 12. Certificate Transparency

One of Assetfinder's useful sources is Certificate Transparency.

Suppose:

```
api.example.com
dev.example.com
vpn.example.com
```

appeared in TLS certificates.

Assetfinder can potentially discover them through CT-related sources.

Conceptually:

```
TLS certificates
       │
       ▼
Certificate Transparency
       │
       ▼
Assetfinder
       │
       ▼
Subdomains
```

This is passive reconnaissance.

---

# 13. API Keys

Some Assetfinder sources require credentials.

For example, the upstream README documents:

### Facebook

```
export FB_APP_ID="your_app_id"
export FB_APP_SECRET="your_app_secret"
```

### VirusTotal

```
export VT_API_KEY="your_api_key"
```

### FindSubdomains / Spyse

```
export SPYSE_API_TOKEN="your_token"
```

These are environment variables consumed by the relevant source integrations. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

Check that they're set:

```
echo "$VT_API_KEY"
```

Avoid putting API keys directly into shell history or public scripts.

---

# 14. Basic Professional Command

For a normal authorized assessment:

```
assetfinder --subs-only example.com | sort -u > subdomains.txt
```

This gives you a clean list:

```
api.example.com
blog.example.com
dev.example.com
mail.example.com
staging.example.com
vpn.example.com
```

---

# 15. Assetfinder → DNS Resolution

Assetfinder finds names.

It doesn't replace a DNS resolver.

For example:

```
assetfinder --subs-only example.com | sort -u | dnsx
```

Conceptually:

```
Assetfinder
     │
     ▼
subdomains
     │
     ▼
dnsx
     │
     ▼
DNS records / IP addresses
```

Or save first:

```
assetfinder --subs-only example.com | sort -u > subdomains.txt
```

Then:

```
cat subdomains.txt | dnsx
```

---

# 16. Assetfinder → HTTPX

This is one of the most useful combinations.

```
assetfinder --subs-only example.com | sort -u | httpx
```

You are essentially asking:

> Which discovered subdomains expose HTTP/HTTPS services?

For example:

```
https://api.example.com
https://dev.example.com
https://portal.example.com
```

Save:

```
assetfinder --subs-only example.com | sort -u | httpx -o live-hosts.txt
```

---

# 17. Assetfinder → Nmap

First:

```
assetfinder --subs-only example.com | sort -u > subdomains.txt
```

Resolve them:

```
cat subdomains.txt | dnsx -resp-only > ips.txt
```

Then, for an authorized target:

```
nmap -iL ips.txt
```

Service detection:

```
nmap -sV -iL ips.txt
```

Workflow:

```
Assetfinder
     ↓
Subdomains
     ↓
DNSX
     ↓
IP addresses
     ↓
Nmap
     ↓
Open ports/services
```

---

# 18. Assetfinder → Nuclei

For an authorized assessment:

```
assetfinder --subs-only example.com | sort -u | httpx -silent | nuclei
```

Pipeline:

```
example.com
     ↓
Assetfinder
     ↓
Subdomains
     ↓
httpx
     ↓
Live web services
     ↓
Nuclei
     ↓
Security checks
```

For a real engagement, keep the Nuclei templates and scan rate within the defined scope.

---

# 19. Assetfinder + Subfinder

Since you're learning both, this is important.

Run:

```
assetfinder --subs-only example.com > assetfinder.txt
```

and:

```
subfinder -d example.com -silent > subfinder.txt
```

Combine:

```
cat assetfinder.txt subfinder.txt | sort -u > combined.txt
```

Now:

```
cat combined.txt
```

gives you the deduplicated result from both tools.

---

# 20. Assetfinder + Amass + Subfinder

A stronger passive enumeration workflow:

```
assetfinder --subs-only example.com > assetfinder.txt

subfinder -d example.com -silent > subfinder.txt

amass enum -passive -d example.com -o amass.txt
```

Combine:

```
cat assetfinder.txt subfinder.txt amass.txt | sort -u > all-subdomains.txt
```

Then:

```
cat all-subdomains.txt | dnsx -silent
```

Pipeline:

```
             example.com
                  │
       ┌──────────┼──────────┐
       ▼          ▼          ▼
 Assetfinder   Subfinder   Amass
       │          │          │
       └──────────┼──────────┘
                  ▼
              sort -u
                  │
                  ▼
          all-subdomains.txt
                  │
                  ▼
                dnsx
                  │
                  ▼
             Resolved hosts
```

---

# 21. Why Use Assetfinder If You Already Have Subfinder?

Good question.

They overlap heavily, but they are different tools.

### Assetfinder

```
Simple
Lightweight
Minimal CLI
Easy to pipe
Good passive source aggregation
```

### Subfinder

```
More feature-rich
More configurable
More passive providers
Source selection
API provider configuration
Filtering
Rate limiting
Recursive enumeration
Structured output
```

Subfinder is explicitly designed as a fast, modular passive subdomain enumerator with extensive source integration and pipeline support. [GitHub](https://github.com/projectdiscovery/subfinder?utm_source=chatgpt.com)

So you can think of Assetfinder as:

> **A small, Unix-friendly passive asset discovery tool.**

And Subfinder as:

> **A more feature-rich passive subdomain enumeration framework.**

---

# 22. Assetfinder vs Subfinder

|Feature|Assetfinder|Subfinder|
|---|---|---|
|Passive enumeration|✅|✅|
|Subdomain discovery|✅|✅|
|Simple CLI|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|
|Source selection|Limited|✅|
|API providers|Some|Many|
|Recursive enumeration|Limited|✅|
|Rate controls|Minimal|✅|
|JSON output|❌/limited|✅|
|Filtering|Shell tools|Built-in|
|Pipeline friendly|✅|✅|
|Lightweight|✅|✅|
|Advanced configuration|Limited|Extensive|

The upstream Assetfinder README itself describes a very small interface: essentially the target domain plus `--subs-only`; its TODO section even notes that source-selection flags were not part of the original design. [GitHub](https://github.com/tomnomnom/assetfinder/blob/master/README.md?utm_source=chatgpt.com)

---

# 23. Assetfinder's Biggest Limitation

Don't confuse:

```
Assetfinder results
```

with:

```
Complete attack surface
```

Example:

```
Actual infrastructure:

api.example.com
dev.example.com
staging.example.com
internal.example.com
vpn.example.com
```

Assetfinder might return only:

```
api.example.com
dev.example.com
vpn.example.com
```

Why?

Passive enumeration depends on information that has been exposed to the underlying sources.

Therefore:

```
Passive discovery
        ≠
Complete discovery
```

This is why professional reconnaissance uses multiple sources and techniques.

---

# 24. Common Mistakes

### Mistake 1 — Forgetting `--subs-only`

Instead of:

```
assetfinder example.com
```

use:

```
assetfinder --subs-only example.com
```

when your goal is specifically subdomain enumeration.

---

### Mistake 2 — Not deduplicating

Use:

```
sort -u
```

Example:

```
assetfinder --subs-only example.com | sort -u
```

---

### Mistake 3 — Treating results as live hosts

A discovered name doesn't necessarily mean:

```
DNS resolves
```

or:

```
HTTP server exists
```

Resolve/probe afterward.

---

### Mistake 4 — Expecting lots of CLI options

Assetfinder intentionally has a minimal interface.

Don't look for options such as:

```
-o
-t
-rl
-json
```

as you would with larger enumeration tools.

Instead, Unix tools handle much of the workflow:

```
assetfinder --subs-only example.com | sort -u > results.txt
```

---

# 25. Useful Shell Combinations

### Count subdomains

```
assetfinder --subs-only example.com | sort -u | wc -l
```

### Save unique results

```
assetfinder --subs-only example.com | sort -u > subdomains.txt
```

### Resolve DNS

```
assetfinder --subs-only example.com | sort -u | dnsx
```

### Find web services

```
assetfinder --subs-only example.com | sort -u | httpx
```

### Save live web services

```
assetfinder --subs-only example.com | sort -u | httpx -silent -o live.txt
```

### Combine with Subfinder

```
assetfinder --subs-only example.com > assetfinder.txt
subfinder -d example.com -silent > subfinder.txt
cat assetfinder.txt subfinder.txt | sort -u > all.txt
```

---

# 26. Recommended Pentesting Workflow

For your red-team/pentesting learning path, remember this workflow:

```
                 TARGET
                    │
                    ▼
          Passive Enumeration
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
     Assetfinder  Subfinder  Amass
          │         │         │
          └─────────┼─────────┘
                    ▼
                 sort -u
                    │
                    ▼
            all-subdomains.txt
                    │
                    ▼
                  dnsx
                    │
             ┌──────┴──────┐
             ▼             ▼
            IPs        DNS records
             │
             ▼
           httpx
             │
             ▼
       Live web services
             │
       ┌─────┴─────┐
       ▼           ▼
     Nuclei       Nmap
```

---

# 27. Commands to Memorize

If you're preparing for pentesting interviews, these are the important ones:

```
# Basic
assetfinder example.com

# Subdomains only
assetfinder --subs-only example.com

# Save
assetfinder --subs-only example.com > subdomains.txt

# Deduplicate
assetfinder --subs-only example.com | sort -u

# Count
assetfinder --subs-only example.com | sort -u | wc -l

# DNS resolution
assetfinder --subs-only example.com | sort -u | dnsx

# HTTP probing
assetfinder --subs-only example.com | sort -u | httpx

# Combine with Subfinder
cat assetfinder.txt subfinder.txt | sort -u
```

## Mental model

```
ASSETFINDER
     │
     │ passive sources
     ▼
SUBDOMAINS
     │
     │ sort -u
     ▼
CLEAN HOST LIST
     │
     ├──────► dnsx ────► IP/DNS
     │
     └──────► httpx ───► Live web hosts
```