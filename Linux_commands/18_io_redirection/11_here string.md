
---
Provides a single string as stdin.

```
wc -w <<< "hello world"
```

Output:

```
2
```

Example:

```
read -r name <<< "Sohan"
echo "$name"
```