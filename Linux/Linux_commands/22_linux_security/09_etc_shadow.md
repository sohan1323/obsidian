
---
Contains password hashes and password-aging information.

```
sudo cat /etc/shadow
```

Typical structure:

```
username:$hash:...
```

Access should normally be restricted.

Check permissions:

```
ls -l /etc/shadow
```


# Password Hash Enumeration

For authorized administration/auditing:

```
sudo awk -F: '{print $1 ":" $2}' /etc/shadow
```

This exposes password hashes, so handle the output securely.