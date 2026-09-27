
---
Reads hardware information from DMI/SMBIOS.

Usually requires root:

```
sudo dmidecode
```

Specific information:

```
sudo dmidecode -t system
```

```
sudo dmidecode -t memory
```

```
sudo dmidecode -t processor
```

```
sudo dmidecode -t bios
```

Useful:

```
sudo dmidecode -s system-product-name
```

```
sudo dmidecode -s bios-version
```