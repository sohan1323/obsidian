
---
`eventcreate` creates a custom event in a Windows event log.

### Syntax

```
eventcreate /ID ID /L LOG /T TYPE /SO SOURCE /D DESCRIPTION
```

Example:

```
eventcreate /ID 100 /L APPLICATION /T INFORMATION /SO LabTest /D "Test event"
```