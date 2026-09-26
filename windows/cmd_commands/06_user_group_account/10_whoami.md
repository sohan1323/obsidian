
---
```
whoami
```

Example:

```
desktop01\sohan
```


# `whoami /user`

Shows the current account's SID.

```
whoami /user
```

Example:

```
User Name       SID
=============== ==========================================
desktop01\sohan S-1-5-21-...
```

### Why SID matters

Windows identifies security principals using **Security Identifiers (SIDs)** rather than relying solely on usernames.

For example:

```
S-1-5-18
```

is the well-known SID for the **Local System** account.



# `whoami /groups`

Displays groups contained in the current security token.

```
whoami /groups
```

You may see groups such as:

```
BUILTIN\Users
BUILTIN\Administrators
NT AUTHORITY\INTERACTIVE
```

The output can also include:

- SID
- attributes
- enabled/deny-only status
- integrity-related information

This is important for understanding what the current process is allowed to do.




# `whoami /priv`

Displays privileges in the current token.

```
whoami /priv
```

Examples include:

```
SeChangeNotifyPrivilege
SeShutdownPrivilege
SeIncreaseWorkingSetPrivilege
```

A privilege is different from a group membership.

Think of:

```
Group membership
        ↓
Who are you / which security groups are you in?

Privileges
        ↓
What special operating-system actions can your token perform?
```





# `whoami /all`

Displays all available identity/token information:

```
whoami /all
```

Conceptually:

```
whoami /all
│
├── User
│   └── SID
│
├── Groups
│   ├── Users
│   ├── Administrators
│   └── ...
│
├── Privileges
│   ├── Se...
│   └── ...
│
└── Token information
```

For Windows security work, this is one of the commands you should become very comfortable with.





# Local User vs Domain User

This distinction is essential.

### Local account

```
COMPUTER01\Sohan
```

The account belongs to the local Windows machine.

### Domain account

```
DOMAIN\Sohan
```

The account is managed by the Active Directory domain.

You can identify your current context with:

```
whoami
```

And inspect system/domain information with:

```
systeminfo
```

You can also inspect:

```
echo %USERDOMAIN%
```

and:

```
echo %LOGONSERVER%
```





# Useful Environment Variables for Accounts

### Current username

```
echo %USERNAME%
```

### User domain

```
echo %USERDOMAIN%
```

### Logon server

```
echo %LOGONSERVER%
```

### Computer

```
echo %COMPUTERNAME%
```

Example:

```
echo User=%USERNAME%
echo Domain=%USERDOMAIN%
echo Computer=%COMPUTERNAME%
echo LogonServer=%LOGONSERVER%
```





# Account Enumeration Workflow

On a Windows machine you are authorized to assess:

```
whoami
whoami /user
whoami /groups
whoami /priv
whoami /all

net user
net localgroup
net localgroup Administrators

net accounts

echo %USERDOMAIN%
echo %LOGONSERVER%
```

This gives you:

```
Current identity
       ↓
SID
       ↓
Groups
       ↓
Privileges
       ↓
Local accounts
       ↓
Local privileged groups
       ↓
Password/account policy
       ↓
Domain/logon context
```