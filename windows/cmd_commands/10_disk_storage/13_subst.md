
---
Maps a directory to a virtual drive letter.

Example:

```
subst X: C:\Lab
```

Now:

```
X:
```

points to:

```
C:\Lab
```

### List substitutions

```
subst
```

### Remove

```
subst X: /d
```

Important distinction:

```
subst
```

maps a **directory** to a virtual drive.

Whereas:

```
net use
```

maps a **network resource**.