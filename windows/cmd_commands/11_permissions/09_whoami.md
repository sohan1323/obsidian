
---
# `whoami`

`whoami` identifies the current security identity.

```
whoami
```

Example:

```
LAB\alice
```


# `whoami /user`

Displays the current user's SID.

```
whoami /user
```

Example:

```
User Name      SID
LAB\alice      S-1-5-21-...
```

A **SID** uniquely identifies a Windows security principal.


# `whoami /groups`

Displays groups associated with the current security token.

```
whoami /groups
```

This can reveal groups such as:

```
BUILTIN\Administrators
BUILTIN\Users
NT AUTHORITY\INTERACTIVE
```

It is important for understanding effective privileges.


# `whoami /priv`

Displays privileges assigned to the current token.

```
whoami /priv
```

Examples of Windows privileges include:

```
SeChangeNotifyPrivilege
SeShutdownPrivilege
SeTimeZonePrivilege
```

Some powerful privileges can have significant security implications.


# `whoami /all`

Displays comprehensive security identity information.

```
whoami /all
```

It combines information about:

- User
- SID
- Groups
- Privileges
- Token information

For Windows security enumeration, this is one of the most useful commands.


# `whoami /upn`

Displays the User Principal Name.

```
whoami /upn
```

Example:

```
alice@corp.example
```

Primarily relevant to domain environments.


# `whoami /fqdn`

Displays the fully qualified domain name associated with the current user when applicable.

```
whoami /fqdn
```


# `whoami /logonid`

Displays the current logon session ID.

```
whoami /logonid
```

Useful when investigating Windows sessions.