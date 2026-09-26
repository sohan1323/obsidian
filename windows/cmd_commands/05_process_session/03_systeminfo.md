
---
Displays detailed Windows system information.

### Syntax

```
systeminfo
```

### Basic

```
systeminfo
```

You'll get information such as:

```
Host Name
OS Name
OS Version
OS Manufacturer
OS Configuration
OS Build Type
Registered Owner
System Boot Time
System Manufacturer
System Model
System Type
Processor(s)
BIOS Version
Windows Directory
System Directory
Boot Device
System Locale
Time Zone
Total Physical Memory
Available Physical Memory
Virtual Memory
Domain
Logon Server
Hotfixes
Network Cards
Hyper-V Requirements
```

This is an important enumeration command.

---

## Search systeminfo output

```
systeminfo | findstr /i "OS Name"
```

```
systeminfo | findstr /i "OS Version"
```

```
systeminfo | findstr /i "System Type"
```

```
systeminfo | findstr /i "Memory"
```

---

## Save system information

```
systeminfo > systeminfo.txt
```