
---
Displays failed login attempts recorded in the bad-login database.

```
sudo lastb
```

Limit:

```
sudo lastb -n 20
```

### Practical security use

Investigate repeated failed authentication attempts:

```
sudo lastb -n 50
```