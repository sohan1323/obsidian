
---
`%*` represents **all arguments** passed to the batch file.

Example:

```
@echo off
echo All arguments: %*
```

Run:

```
test.bat one two three four
```

Output:

```
All arguments: one two three four
```