
---
Google dorking (Google hacking) is the use of **advanced Google search operators** to narrow search results and discover information that ordinary searches may miss.

For authorized security testing, it is useful during **OSINT, reconnaissance, attack-surface discovery, and exposure assessment**.

---

## 1. Basic Google Search Syntax

```
keyword
```

Example:

```
cybersecurity
```

Search multiple words:

```
cybersecurity pentesting
```

Exact phrase:

```
"penetration testing"
```

Exclude a word:

```
pentesting -course
```

OR:

```
pentesting OR cybersecurity
```

Group terms:

```
("penetration testing" OR "red team") training
```

---

# 2. `site:`

Restricts results to a particular domain.

### Syntax

```
site:domain.com keyword
```

Example:

```
site:example.com login
```

Search only a specific subdomain:

```
site:dev.example.com
```

Search a country-code domain:

```
site:gov.in cybersecurity
```

Search multiple domains:

```
site:example.com OR site:example.org
```

### Pentesting use

Find publicly indexed pages belonging to an authorized target:

```
site:example.com
```

Then narrow it:

```
site:example.com admin
```

```
site:example.com login
```

```
site:example.com api
```

---

# 3. `intitle:`

Searches for terms appearing in the page title.

### Syntax

```
intitle:keyword
```

Example:

```
intitle:"login"
```

Multiple words:

```
intitle:"login" portal
```

Multiple title conditions:

```
intitle:admin intitle:login
```

### Useful reconnaissance searches

```
site:example.com intitle:login
```

```
site:example.com intitle:dashboard
```

```
site:example.com intitle:"admin panel"
```

---

# 4. `allintitle:`

All specified words must appear in the title.

```
allintitle:admin login
```

Compared with:

```
intitle:admin login
```

`allintitle:` applies the operator to all following terms.

---

# 5. `inurl:`

Searches for terms appearing in the URL.

### Syntax

```
inurl:keyword
```

Examples:

```
inurl:login
```

```
inurl:admin
```

```
inurl:dashboard
```

```
inurl:api
```

Authorized-target reconnaissance:

```
site:example.com inurl:admin
```

```
site:example.com inurl:login
```

```
site:example.com inurl:api
```

---

# 6. `allinurl:`

All specified terms are searched for in URLs.

```
allinurl:admin login
```

Useful for identifying URL patterns.

---

# 7. `intext:`

Searches for text appearing in the page.

```
intext:"internal use only"
```

```
intext:"confidential"
```

Target-specific:

```
site:example.com intext:"internal"
```

---

# 8. `allintext:`

All specified terms are searched for within page text.

```
allintext:internal confidential
```

---

# 9. `filetype:`

Searches for a particular file type.

### Syntax

```
filetype:extension
```

Examples:

```
filetype:pdf
```

```
filetype:docx
```

```
filetype:xlsx
```

Target-specific:

```
site:example.com filetype:pdf
```

```
site:example.com filetype:xlsx
```

### Security assessment

You can use this to identify documents unintentionally exposed by an authorized organization's website:

```
site:example.com filetype:pdf
```

```
site:example.com filetype:xlsx
```

```
site:example.com filetype:docx
```

---

# 10. `ext:`

Alternative syntax for file extensions.

```
site:example.com ext:pdf
```

```
site:example.com ext:xlsx
```

---

# 11. `before:` and `after:`

Restrict results by date.

```
site:example.com after:2025-01-01
```

```
site:example.com before:2025-01-01
```

Combined:

```
site:example.com after:2025-01-01 before:2026-01-01
```

Useful when investigating historical exposure.

---

# 12. `cache:` / Cached Results

Historically, Google supported:

```
cache:example.com
```

However, **Google's cache feature has been discontinued**, so don't rely on `cache:` in modern workflows.

---

# 13. Quotes `" "`

Exact phrase matching.

```
"internal server"
```

```
"confidential document"
```

Target:

```
site:example.com "internal documentation"
```

This is particularly useful when searching for a known phrase.

---

# 14. Minus `-`

Exclude results.

```
site:example.com -blog
```

Exclude several terms:

```
site:example.com -blog -news -careers
```

Example:

```
penetration testing -course -training
```

---

# 15. `OR`

Search for either condition.

```
admin OR administrator
```

Combine with `site:`:

```
site:example.com admin OR administrator
```

Better grouping:

```
site:example.com (admin OR administrator)
```

---

# 16. Wildcard `*`

The `*` can act as a wildcard in phrases.

```
"best * security tools"
```

For example:

```
"welcome to * portal"
```

Results can contain different words in the wildcard position.

---

# 17. Parentheses `( )`

Used to group search conditions.

Example:

```
site:example.com (login OR admin OR dashboard)
```

Another:

```
site:example.com (pdf OR doc OR xls)
```

This becomes particularly useful when building larger queries.

---

# 18. Combining Operators

The real power of Google dorking comes from combining operators.

### Example

```
site:example.com intitle:login
```

Meaning:

> Search `example.com` for pages whose title contains "login".

---

### URL + site

```
site:example.com inurl:admin
```

---

### File + site

```
site:example.com filetype:pdf
```

---

### Multiple conditions

```
site:example.com (inurl:login OR inurl:admin)
```

---

### Exact phrase + site

```
site:example.com "internal documentation"
```

---

# 19. Reconnaissance Workflow

For an **authorized target**, don't start with complicated dorks.

Start broad.

### Step 1 — Discover indexed pages

```
site:example.com
```

### Step 2 — Find authentication pages

```
site:example.com (inurl:login OR inurl:signin)
```

### Step 3 — Find administrative interfaces

```
site:example.com (inurl:admin OR intitle:admin)
```

### Step 4 — Find APIs

```
site:example.com (inurl:api OR inurl:swagger)
```

### Step 5 — Find documents

```
site:example.com (filetype:pdf OR filetype:docx OR filetype:xlsx)
```

### Step 6 — Search specific terminology

```
site:example.com "internal"
```

```
site:example.com "confidential"
```

### Step 7 — Investigate historical exposure

```
site:example.com after:2024-01-01 before:2025-01-01
```

---

# 20. Finding Common Technology Indicators

Search for publicly indexed technology-related pages.

```
site:example.com "powered by"
```

```
site:example.com "Apache"
```

```
site:example.com "nginx"
```

```
site:example.com "Django"
```

```
site:example.com "WordPress"
```

These aren't reliable technology fingerprints by themselves, but they can provide reconnaissance leads.

---

# 21. Finding Development/Documentation Pages

```
site:example.com inurl:docs
```

```
site:example.com inurl:documentation
```

```
site:example.com inurl:swagger
```

```
site:example.com inurl:api
```

```
site:example.com inurl:dev
```

```
site:example.com inurl:test
```

---

# 22. Finding Login-Related Pages

```
site:example.com inurl:login
```

```
site:example.com inurl:signin
```

```
site:example.com inurl:auth
```

```
site:example.com intitle:login
```

Combined:

```
site:example.com (inurl:login OR inurl:signin OR inurl:auth)
```

---

# 23. Finding Exposed Documents

For authorized assessment:

```
site:example.com filetype:pdf
```

```
site:example.com filetype:xlsx
```

```
site:example.com filetype:docx
```

```
site:example.com filetype:csv
```

Then search for specific terms:

```
site:example.com filetype:pdf "internal"
```

```
site:example.com filetype:xlsx "employee"
```

---

# 24. Finding Potentially Forgotten Pages

```
site:example.com inurl:test
```

```
site:example.com inurl:dev
```

```
site:example.com inurl:staging
```

```
site:example.com inurl:old
```

```
site:example.com inurl:backup
```

These are **reconnaissance queries**, not proof that a vulnerable system exists.

---

# 25. Searching for Error Pages

Useful during authorized reconnaissance:

```
site:example.com "error"
```

```
site:example.com "exception"
```

```
site:example.com "stack trace"
```

```
site:example.com "debug"
```

```
site:example.com "Internal Server Error"
```

These can sometimes reveal information about application technologies or deployment mistakes.

---

# 26. Google Dork Categories

For pentesting, think in categories rather than memorizing hundreds of individual queries.

|Category|Operators|
|---|---|
|Domain discovery|`site:`|
|URL discovery|`inurl:`|
|Title discovery|`intitle:`|
|Content discovery|`intext:`|
|Documents|`filetype:` / `ext:`|
|Exact phrases|`"..."`|
|Exclusions|`-`|
|Alternatives|`OR`|
|Grouping|`( )`|
|Date filtering|`before:` / `after:`|

---

# 27. Building a Dork Step-by-Step

Instead of memorizing a giant query, construct it.

Suppose your authorized target is:

```
example.com
```

Start:

```
site:example.com
```

Add a resource type:

```
site:example.com login
```

Restrict the URL:

```
site:example.com inurl:login
```

Add alternatives:

```
site:example.com (inurl:login OR inurl:signin)
```

Add title filtering:

```
site:example.com (intitle:login OR intitle:signin)
```

Add exclusions:

```
site:example.com (inurl:login OR inurl:signin) -blog
```

This approach is much more useful professionally than memorizing random "Google dorks."

---

# 28. Important Limitation

Google dorking is **not a vulnerability scanner**.

Finding:

```
site:example.com inurl:admin
```

does **not** mean:

> "The admin panel is vulnerable."

It only means that Google has indexed a page matching the search criteria.

Likewise:

```
site:example.com filetype:xlsx
```

doesn't automatically mean the spreadsheet contains sensitive information.

You must validate findings through your authorized testing methodology.

---

# 29. Professional Workflow

A practical workflow is:

```
Target
  ↓
Google indexing
  ↓
site:
  ↓
Subdomains / pages
  ↓
inurl:
  ↓
Interesting endpoints
  ↓
intitle:
  ↓
filetype:
  ↓
Documents / exposed resources
  ↓
intext:
  ↓
Interesting information
  ↓
Manual validation
  ↓
Document finding
```

---

# 30. Quick Cheatsheet

```
site:example.com
```

Domain restriction.

```
site:example.com inurl:login
```

Find login URLs.

```
site:example.com intitle:login
```

Find pages with "login" in title.

```
site:example.com inurl:admin
```

Find admin-related URLs.

```
site:example.com filetype:pdf
```

Find PDFs.

```
site:example.com filetype:xlsx
```

Find Excel documents.

```
site:example.com "internal"
```

Find exact phrase.

```
site:example.com intext:"confidential"
```

Search page content.

```
site:example.com (login OR signin)
```

Search alternatives.

```
site:example.com -blog
```

Exclude blog results.

```
site:example.com after:2025-01-01
```

Results after a date.

```
site:example.com before:2026-01-01
```

Results before a date.

```
site:example.com (inurl:dev OR inurl:test OR inurl:staging)
```

Look for development/test/staging references.

```
site:example.com (inurl:api OR inurl:swagger OR inurl:docs)
```

Look for API/documentation references.

---

## The key skill

Don't try to memorize 500 dorks.

Learn this construction pattern:

```
[scope] + [location] + [content] + [file/type] + [filter]
```

For example:

```
site:example.com + inurl:api + "swagger"
```

becomes:

```
site:example.com inurl:api "swagger"
```

Once you understand the operators, you can construct new queries yourself for almost any reconnaissance objective.