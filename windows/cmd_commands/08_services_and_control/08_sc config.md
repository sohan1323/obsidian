
---
Changes service configuration.

This is one of the most important `sc` commands.

### Syntax

```
sc config ServiceName [option=value]
```

**Important:** `sc` requires a space between the option and its value format:

```
start= auto
```

not:

```
start=auto
```

---

## `start=`

Controls the startup type.

Possible values include:

```
boot
system
auto
demand
disabled
```

### Automatic

```
sc config MyService start= auto
```

### Manual / demand

```
sc config MyService start= demand
```

### Disabled

```
sc config MyService start= disabled
```

Check afterward:

```
sc qc MyService
```

---

## `binPath=`

Changes the executable path.

```
sc config MyService binPath= "C:\Program Files\MyApp\service.exe"
```

This is a sensitive configuration because it determines what executable the SCM launches.

For legitimate administration, verify the intended executable before changing it.

---

## `obj=`

Changes the account under which the service runs.

Example:

```
sc config MyService obj= ".\LocalService"
```

Another common service account:

```
sc config MyService obj= "NT AUTHORITY\LocalService"
```

Changing service accounts can affect permissions and service functionality.

---

## `depend=`

Specifies dependencies.

Example:

```
sc config MyService depend= Tcpip
```

Multiple dependencies can be specified using `/`.

```
sc config MyService depend= Tcpip/Afd
```

---

## `displayname=`

Changes the service's display name.

```
sc config MyService displayname= "My Application Service"
```

---

## `type=`

Controls service type.

Example:

```
sc config MyService type= own
```

Common values include:

```
own
share
interact
kernel
filesys
rec
userown
usershare
```

Do not change service type casually; it can prevent a service from starting correctly.