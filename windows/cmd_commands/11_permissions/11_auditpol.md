
---
`auditpol` manages and queries Windows advanced audit policy.

### Display audit policy

```
auditpol /get /category:*
```

This can produce a large amount of information.


# `auditpol /get`

### Get all categories

```
auditpol /get /category:*
```

### Get a specific category

```
auditpol /get /category:"Logon/Logoff"
```

### Get system category

```
auditpol /get /category:"System"
```

# `auditpol /set`

Changes audit policy.

Example:

```
auditpol /set /subcategory:"Logon" /success:enable
```

Enable failure auditing:

```
auditpol /set /subcategory:"Logon" /failure:enable
```

Both:

```
auditpol /set /subcategory:"Logon" /success:enable /failure:enable
```

Audit policy changes should be made deliberately because they affect security logging.


# `auditpol /list`

List available categories/subcategories.

```
auditpol /list /category
```

List subcategories:

```
auditpol /list /subcategory:*
```

# `auditpol /backup`

Back up audit policy.

```
auditpol /backup /file:C:\Lab\audit-policy.csv
```

# `auditpol /restore`

Restore an audit policy.

```
auditpol /restore /file:C:\Lab\audit-policy.csv
```


# `auditpol /clear`

Clears audit policy settings.

```
auditpol /clear
```

This is an administrative operation and should not be used casually because it changes security auditing.