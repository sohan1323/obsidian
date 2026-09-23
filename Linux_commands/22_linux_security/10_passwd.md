
---
Manage passwords.

Change your password:

```
passwd
```

Change another user's password as root:

```
sudo passwd username
```

Lock account:

```
sudo passwd -l username
```

Unlock:

```
sudo passwd -u username
```

Delete password:

```
sudo passwd -d username
```

Password deletion can create a serious authentication weakness and should only be done deliberately.




# Account Expiration

Check password/account status:

```
sudo passwd -S username
```

Detailed aging:

```
sudo chage -l username
```

Change password expiration:

```
sudo chage -M 90 username
```

Set account expiration:

```
sudo chage -E 2026-12-31 username
```