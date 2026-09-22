
---
### Find failed logins

```
grep "Failed password" /var/log/auth.log
```

Count them:

```
grep "Failed password" /var/log/auth.log | wc -l
```

Find unique source IPs:

```
grep "Failed password" /var/log/auth.log \
| awk '{print $11}' \
| sort -u
```

Count source IPs:

```
grep "Failed password" /var/log/auth.log \
| awk '{print $11}' \
| sort \
| uniq -c \
| sort -nr
```

### Extract usernames

```
cut -d ':' -f 1 /etc/passwd
```

Equivalent with `awk`:

```
awk -F ':' '{print $1}' /etc/passwd
```

### Search recursively and count matches

```
grep -r "password" /etc 2>/dev/null | wc -l
```

### Save output while displaying it

```
ps aux | tee processes.txt
```