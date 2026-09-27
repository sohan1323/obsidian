
---
Breaks a path into its components and displays permissions.

```
namei /var/log/auth.log
```

Example conceptually:

```
/
└── var
    └── log
        └── auth.log
```

This is particularly useful for permission troubleshooting.

For a symlink:

```
namei -l /path/to/file
```

The `-l` option shows permissions for each path component.