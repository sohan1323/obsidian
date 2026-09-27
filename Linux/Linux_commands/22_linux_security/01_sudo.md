
---
`sudo` executes a command with elevated privileges according to the sudo policy.

```
sudo command
```

Example:

```
sudo systemctl restart nginx
```

Run as another user:

```
sudo -u username command
```

Run a root login shell:

```
sudo -i
```

Check permitted commands:

```
sudo -l
```

`sudo -l` is particularly important during authorized privilege-assessment work.