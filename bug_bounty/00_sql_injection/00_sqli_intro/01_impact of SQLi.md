
---
A successful SQL injection can have **severe impact**, depending on the application's database permissions and how the vulnerability can be exploited.

- **Authentication bypass** — log in without valid credentials.
- **Data disclosure** — retrieve sensitive data such as usernames, passwords, emails, tokens, or financial information.
- **Data modification** — alter existing database records.
- **Data deletion** — delete records or entire tables.
- **Privilege escalation** — modify roles or permissions in the application's data.
- **Database takeover** — in some cases, gain extensive control over the database.
- **Server-level compromise** — certain database configurations/features may allow SQLi to lead to operating-system command execution.
- **Denial of service** — corrupt or delete data, consume database resources, or otherwise make the application unavailable.