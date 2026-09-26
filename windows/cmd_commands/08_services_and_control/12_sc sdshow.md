
---
Displays a service's security descriptor.

### Syntax

```
sc sdshow ServiceName
```

Example:

```
sc sdshow Spooler
```

Output resembles:

```
D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)...
```

This is an **SDDL security descriptor**.

It controls who can perform operations such as:

- start
- stop
- query
- change configuration
- delete

### Security relevance

When auditing services, service permissions are important.

For example:

```
sc sdshow MyService
```

can help determine how the service is secured.