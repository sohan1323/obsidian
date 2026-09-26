
---
`qwinsta` means **Query WINdows STAtion**.

### Purpose

Displays information about sessions.

### Basic

```
qwinsta
```

Example:

```
SESSIONNAME       USERNAME        ID STATE
console           sohan            1 Active
rdp-tcp#1         admin            2 Active
```

### Compare

```
quser
  ↓
Users

qwinsta
  ↓
Sessions
```

They overlap significantly.