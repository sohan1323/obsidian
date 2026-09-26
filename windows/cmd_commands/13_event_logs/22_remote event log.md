
---
`wevtutil` can query logs on another computer when you have the necessary permissions and remote event-log access.

General pattern:

```
wevtutil qe System /r:SERVER01
```

Example:

```
wevtutil qe System /r:SERVER01 /c:10 /rd:true /f:text
```

Remote authentication/configuration can vary by Windows environment.


# `/u` and `/p`

Credentials can be specified for remote operations where supported.

Example pattern:

```
wevtutil qe System /r:SERVER01 /u:DOMAIN\Alice /p:*
```

`*` causes Windows to prompt for the password rather than placing it directly in the command line.

Avoid putting real passwords directly into commands because command history and process inspection can expose credentials.