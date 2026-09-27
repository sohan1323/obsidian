
---
On Debian/Ubuntu/Kali systems, authentication-related events are commonly recorded here.

View:

```
sudo less /var/log/auth.log
```

Search failed authentication:

```
sudo grep -i "failed" /var/log/auth.log
```

SSH failures:

```
sudo grep "Failed password" /var/log/auth.log
```

Successful SSH authentication:

```
sudo grep "Accepted" /var/log/auth.log
```

### Practical security use

Identify repeated authentication failures:

```
sudo grep "Failed password" /var/log/auth.log
```

Extract source IPs:

```
sudo grep "Failed password" /var/log/auth.log |
awk '{print $(NF-3)}'
```

A more robust approach depends on the exact log format, so inspect the actual lines before writing field-based parsing.