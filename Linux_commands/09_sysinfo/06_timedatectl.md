
---
### Purpose

Displays and manages system date, time, timezone, and NTP synchronization.

### Syntax

```
timedatectl [COMMAND]
```

### Examples

```
timedatectl
```

Shows:

- Local time
- Universal time
- RTC time
- Time zone
- NTP status
- system clock synchronization

List available timezones:

```
timedatectl list-timezones
```

Search:

```
timedatectl list-timezones | grep Asia
```

Set timezone:

```
sudo timedatectl set-timezone Asia/Kolkata
```

Enable NTP:

```
sudo timedatectl set-ntp true
```

### Practical use

Check whether system time synchronization is working:

```
timedatectl
```

Correct time synchronization is important for authentication systems and logs.