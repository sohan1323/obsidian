
---
The Registry is organized roughly like:

```
Registry
│
├── HKEY_LOCAL_MACHINE (HKLM)
│   ├── SYSTEM
│   ├── SOFTWARE
│   └── SECURITY
│
├── HKEY_CURRENT_USER (HKCU)
│
├── HKEY_CLASSES_ROOT (HKCR)
│
├── HKEY_USERS (HKU)
│
└── HKEY_CURRENT_CONFIG (HKCC)
```

Think of the structure as:

```
Hive
 ↓
Key
 ↓
Subkey
 ↓
Value
```

Example:

```
HKLM
 └── SOFTWARE
      └── Microsoft
           └── Windows
                └── CurrentVersion
```

A registry value has:

```
Name
Type
Data
```

Example:

```
"ProgramFilesDir"    REG_SZ    "C:\Program Files"
```