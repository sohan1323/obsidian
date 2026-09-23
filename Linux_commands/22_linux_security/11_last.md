
---
Shows successful login history.

```
last
```

Limit results:

```
last -n 10
```

Useful during authentication investigations.



# `lastb`

Shows failed login attempts, using the system's failed-login database when available.

```
sudo lastb
```

Limit results:

```
sudo lastb -n 20
```




# `lastlog`

Shows the most recent login for users.

```
lastlog
```

Specific user:

```
lastlog -u username
```

This can help identify accounts that haven't logged in recently.