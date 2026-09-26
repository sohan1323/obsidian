
---
Query another machine:

```
schtasks /query /s SERVER01 /fo list /v
```

With credentials:

```
schtasks /query /s SERVER01 /u DOMAIN\Alice /p *
```

Remote task management requires appropriate administrative permissions.