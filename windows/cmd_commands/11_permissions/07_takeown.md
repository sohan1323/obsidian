
---
`takeown` allows an administrator to take ownership of files/directories.

### Basic syntax

```
takeown /f Path
```

Example:

```
takeown /f C:\Lab\file.txt
```

---

## `/r`

Recursively process directories.

```
takeown /f C:\Lab /r
```

---

## `/d`

Specifies the response to prompts encountered while recursively processing.

Example:

```
takeown /f C:\Lab /r /d Y
```

---

## `/a`

Assign ownership to the Administrators group instead of the current user.

```
takeown /f C:\Lab /r /a
```