
---
Think of the structure as:

```
Event Log
   │
   ├── Channel
   │      └── Security
   │      └── System
   │      └── Application
   │
   └── Event
          ├── Event ID
          ├── Provider
          ├── Level
          ├── Time
          ├── User
          └── Event Data
```

Common logs:

| Log               | Purpose                              |
| ----------------- | ------------------------------------ |
| `Application`     | Application events                   |
| `System`          | Windows/system events                |
| `Security`        | Authentication and security auditing |
| `Setup`           | Windows setup events                 |
| `ForwardedEvents` | Forwarded events                     |
