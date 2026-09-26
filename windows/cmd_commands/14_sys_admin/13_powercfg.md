
---
`powercfg` manages Windows power configuration.

### List power plans

```
powercfg /list
```

### Active plan

```
powercfg /getactivescheme
```

### Change active plan

```
powercfg /setactive SCHEME_GUID
```

Example:

```
powercfg /setactive 381b4222-f694-41f0-9685-ff5bb260df2e
```

Use the GUID shown by `/list`.


# `powercfg /hibernate`

Enable hibernation:

```
powercfg /hibernate on
```

Disable:

```
powercfg /hibernate off
```


# `powercfg /batteryreport`

Generates a battery report.

```
powercfg /batteryreport
```

Specify output:

```
powercfg /batteryreport /output C:\Lab\battery.html
```

Open:

```
start C:\Lab\battery.html
```


# `powercfg /energy`

Analyzes power efficiency.

```
powercfg /energy
```

Specify output:

```
powercfg /energy /output C:\Lab\energy.html
```

Windows usually performs the analysis for a short period and produces an HTML report.


# `powercfg /requests`

Shows applications/drivers currently preventing sleep or other power transitions.

```
powercfg /requests
```

This is useful when diagnosing:

> "Why won't my computer sleep?"


# `powercfg /sleepstudy`

On supported systems:

```
powercfg /sleepstudy
```

This generates information about Modern Standby behavior.


# `powercfg /a`

Displays available sleep states.

```
powercfg /a
```

Example states may include:

```
Standby
Hibernate
Fast Startup
```


# `shutdown`

Controls system shutdown/restart/logoff operations.

### Shutdown

```
shutdown /s
```

### Restart

```
shutdown /r
```

### Log off

```
shutdown /l
```

### Hibernate

```
shutdown /h
```

# `/t`

Specifies delay in seconds.

```
shutdown /s /t 60
```

Schedules shutdown in 60 seconds.

Cancel:

```
shutdown /a
```

# `/f`

Forces applications to close.

```
shutdown /s /f
```

Use carefully because unsaved work can be lost.

# `/m`

Specifies a remote computer.

```
shutdown /r /m \\SERVER01
```

Administrative permissions are required for remote shutdown.

# `/c`

Adds a comment/reason.

```
shutdown /s /t 60 /c "Scheduled maintenance"
```