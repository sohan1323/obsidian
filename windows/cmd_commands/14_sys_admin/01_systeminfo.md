
---
Displays detailed Windows system information.

### Basic

```
systeminfo
```

It can show:

- Host name
- OS name/version
- OS build
- System manufacturer/model
- BIOS
- CPU
- RAM
- Network configuration
- Windows installation date
- Boot time
- Hotfixes
- Domain/workgroup

---

## Filter output

Combine with `findstr`:

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
systeminfo | findstr /i "Total Physical Memory"
```

---

## Remote system

```
systeminfo /s SERVER01
```

Specify credentials:

```
systeminfo /s SERVER01 /u DOMAIN\Alice
```

Password prompt:

```
systeminfo /s SERVER01 /u DOMAIN\Alice /p *
```