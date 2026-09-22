
---
**Purpose:** Show historical login sessions.

### Syntax

```
last [OPTIONS] [USER]
```

Example:

```
last
```

Possible output:

```
sohan   pts/0   192.168.1.20   Mon Sep 22 14:30
alice   pts/1   192.168.1.30   Mon Sep 22 13:10
```

Check one user:

```
last alice
```

### Important options

|Option|Meaning|
|---|---|
|`-n N`|Show N entries|
|`-i`|Show IP address|
|`-x`|Show shutdown/runlevel information|
|`-F`|Full login/logout times|

Example:

```
last -n 10
```

### Security use

Useful when investigating:

- Unexpected logins
- Remote access
- Login history
- Reboots
- Account activity