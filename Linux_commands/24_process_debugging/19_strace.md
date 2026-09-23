
---
`strace` traces **system calls** made by a process.

Example:

```
strace ls
```

You will see system calls such as:

```
openat()
read()
write()
close()
stat()
```