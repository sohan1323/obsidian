
---
Registry keys themselves have security descriptors.

You can use:

```
regini
```

for certain registry permission-management tasks.

However, modern Windows administration commonly uses PowerShell and security APIs for more detailed registry ACL management.

The important conceptual model is:

```
Registry Key
     ↓
Security Descriptor
     ↓
DACL
     ↓
Users / Groups
     ↓
Allowed / Denied Operations
```