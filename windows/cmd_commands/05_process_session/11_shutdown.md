
---
Shuts down, restarts, logs off, or hibernates Windows.

### Syntax

```
shutdown [/i | /l | /s | /sg | /r | /g | /a | /p | /h | /hybrid] [/f] [/m \\computer] [/t seconds] [/d reason] [/c comment]
```

### `/s`

Shutdown:

```
shutdown /s
```

### `/r`

Restart:

```
shutdown /r
```

### `/l`

Log off current user:

```
shutdown /l
```

### `/h`

Hibernate:

```
shutdown /h
```

### `/a`

Abort a pending shutdown:

```
shutdown /a
```

### `/t`

Specify delay.

```
shutdown /s /t 60
```

Schedules shutdown in 60 seconds.

Cancel it:

```
shutdown /a
```

### `/f`

Force applications to close.

```
shutdown /s /f /t 0
```

Be careful: unsaved application data may be lost.

### `/m`

Specify another computer:

```
shutdown /r /m \\COMPUTER01
```

This requires the appropriate remote permissions and configuration.