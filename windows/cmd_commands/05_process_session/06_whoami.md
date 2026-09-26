
---
One of the most important Windows commands.

### Purpose

Displays the currently logged-in user and security identity.

### Syntax

```
whoami [/user] [/groups] [/priv] [/all] [/fo format] [/upn] [/fqdn]
```

---

## Basic

```
whoami
```

Example:

```
desktop-abc123\sohan
```

---

## `/user`

Displays the user's SID.

```
whoami /user
```

Example:

```
USER INFORMATION
----------------
User Name        SID
================ =========================================
desktop\sohan    S-1-5-21-...
```

---

## `/groups`

Displays group memberships.

```
whoami /groups
```

This can reveal memberships such as:

```
Users
Administrators
Remote Desktop Users
...
```

---

## `/priv`

Displays privileges assigned to the current token.

```
whoami /priv
```

Examples of Windows privileges you may encounter:

```
SeChangeNotifyPrivilege
SeShutdownPrivilege
SeIncreaseWorkingSetPrivilege
```

Some privileges are security-sensitive.

---

## `/all`

Displays comprehensive identity information:

```
whoami /all
```

This includes:

- username
- SID
- groups
- privileges
- claims
- integrity information

This is particularly important for Windows security analysis.

---

## `/upn`

Displays the User Principal Name.

```
whoami /upn
```

Useful in domain environments.

---

## `/fqdn`

Displays the fully qualified domain name associated with the account when applicable.

```
whoami /fqdn
```