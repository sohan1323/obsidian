
---
Displays, creates, modifies, or deletes Windows user accounts.

### Syntax

```
net user
net user username
net user username [password | *] [options]
net user username /add
net user username /delete
```

---

## List local users

```
net user
```

Example:

```
User accounts for \\DESKTOP-ABC123

-------------------------------------------------------------------------------
Administrator
DefaultAccount
Guest
Sohan
```

This is one of the most important basic Windows enumeration commands.

---

## Display a specific user's information

```
net user Sohan
```

Information may include:

```
User name
Full Name
Comment
Account active
Account expires
Password last set
Password expires
Password required
Last logon
Local Group Memberships
Global Group memberships
```

---

## Create a user

```
net user TestUser /add
```

Windows will create the account.

You can specify a password:

```
net user TestUser MyPassword123 /add
```

However, avoid putting real passwords directly into command history or scripts.

A safer interactive form is:

```
net user TestUser * /add
```

CMD prompts for the password rather than displaying it directly.

---

## Delete a user

```
net user TestUser /delete
```

---

## Disable/enable an account

Disable:

```
net user TestUser /active:no
```

Enable:

```
net user TestUser /active:yes
```

---

## Set account expiration

```
net user TestUser /expires:12/31/2026
```

Date interpretation can depend on the system's regional configuration.

To make an account never expire:

```
net user TestUser /expires:never
```

---

## Set password

```
net user TestUser *
```

CMD prompts for the new password.

You can also specify one directly:

```
net user TestUser Password123
```

but this is not recommended for real credentials because command lines can potentially be exposed through history, process inspection, logging, or other mechanisms.

---

## `/passwordchg`

Control whether the user can change their password.

```
net user TestUser /passwordchg:no
```

Enable:

```
net user TestUser /passwordchg:yes
```

---

## `/passwordreq`

Controls whether the account requires a password.

```
net user TestUser /passwordreq:yes
```

or:

```
net user TestUser /passwordreq:no
```

Security-sensitive setting: accounts without passwords should generally be avoided.

---

## `/comment`

Add a comment:

```
net user TestUser /comment:"Test account"
```

---

## `/fullname`

Set the full name:

```
net user TestUser /fullname:"Windows Lab User"
```

---

## `/homedir`

Specify a home directory:

```
net user TestUser /homedir:C:\Users\TestUser
```

---

## `/times`

Controls permitted logon times.

```
net user TestUser /times:M-F,09:00-17:00
```

This is an administrative account-policy feature.