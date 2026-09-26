
---
`>>` appends output.

```
echo First > test.txt
echo Second >> test.txt
echo Third >> test.txt
```

Result:

```
First
Second
Third
```

This is commonly used for logging.

```
echo [%DATE% %TIME%] Script started >> script.log
```