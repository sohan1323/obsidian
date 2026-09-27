
---
Example: count failed SSH attempts by source IP.

First inspect the actual format:

```
sudo grep "Failed password" /var/log/auth.log | head
```

Then extract the appropriate field based on your system's log format.

For a typical OpenSSH Debian-style entry:

```
sudo grep "Failed password" /var/log/auth.log |
awk '{print $(NF-3)}' |
sort |
uniq -c |
sort -nr
```

The general pipeline is:

```
grep
 ↓
extract field
 ↓
sort
 ↓
uniq -c
 ↓
sort -nr
```