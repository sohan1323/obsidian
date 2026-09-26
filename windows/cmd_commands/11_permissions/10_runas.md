
---
Runs a program under another user's credentials.

### Syntax

```
runas /user:USERNAME program
```

Example:

```
runas /user:Administrator cmd.exe
```

Windows will prompt for the password.

---

## `/user:`

Specify the user.

```
runas /user:LAB\alice cmd.exe
```

Local computer:

```
runas /user:COMPUTER01\alice cmd.exe
```


# `runas /profile`

Loads the user's profile.

```
runas /user:LAB\alice /profile cmd.exe
```

This is generally the default behavior.


# `runas /noprofile`

Doesn't load the user's profile.

```
runas /user:LAB\alice /noprofile cmd.exe
```

Useful when you want to avoid loading profile-specific configuration.


# `runas /netonly`

Uses supplied credentials only for remote access.

```
runas /user:DOMAIN\alice /netonly cmd.exe
```

The local process runs under the current local identity, while the supplied credentials are used for network authentication.

This is useful in legitimate domain administration/testing scenarios.