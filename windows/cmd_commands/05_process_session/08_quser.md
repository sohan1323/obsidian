
---
`quser` means **Query User**.

### Purpose

Displays information about logged-in users.

### Syntax

```
quser [username | sessionname | sessionid]
```

### Basic

```
quser
```

Example:

```
USERNAME       SESSIONNAME        ID  STATE
sohan          console             1  Active
admin          rdp-tcp#2           2  Active
```

### Query a specific user

```
quser sohan
```

### Security relevance

This is useful when determining which accounts currently have interactive sessions on a Windows system you are authorized to administer or assess.