
---
Starts a new instance of the Windows command interpreter.

### Syntax

```
cmd [/c | /k] [/q] [/a | /u] [/s] [/d] [/e:on | /e:off] [/f:on | /f:off] [/v:on | /v:off] [command]
```

### Important arguments

|Argument|Meaning|
|---|---|
|`/c`|Execute command and exit|
|`/k`|Execute command and remain open|
|`/q`|Disable echo|
|`/a`|Use ANSI output|
|`/u`|Use Unicode output|
|`/d`|Don't execute AutoRun commands|
|`/e:on`|Enable command extensions|
|`/e:off`|Disable command extensions|
|`/f:on`|Enable filename/directory completion|
|`/v:on`|Enable delayed environment-variable expansion|

### `/c`

Execute command and exit:

```
cmd /c dir
```

Useful when another program needs to execute a CMD command.

### `/k`

Execute command but remain open:

```
cmd /k echo Hello
```

### `/d`

Prevent registry-defined AutoRun commands:

```
cmd /d
```

This can be useful when troubleshooting CMD startup behavior.

### Delayed expansion

```
cmd /v:on
```

This enables:

```
!VARIABLE!
```

which becomes important in advanced batch scripting.