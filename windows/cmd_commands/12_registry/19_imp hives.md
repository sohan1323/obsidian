
---
## `HKLM`

```
HKEY_LOCAL_MACHINE
```

Machine-wide configuration.

Common areas:

```
HKLM\SOFTWARE
HKLM\SYSTEM
HKLM\SECURITY
```

---

## `HKCU`

```
HKEY_CURRENT_USER
```

Settings for the currently logged-in user.

Example:

```
reg query HKCU\Software
```

---

## `HKCR`

```
HKEY_CLASSES_ROOT
```

File associations and COM-related registration.

Example:

```
reg query HKCR\.txt
```

---

## `HKU`

```
HKEY_USERS
```

Contains loaded user profiles.

```
reg query HKU
```

---

## `HKCC`

```
HKEY_CURRENT_CONFIG
```

Current hardware configuration.

```
reg query HKCC
```