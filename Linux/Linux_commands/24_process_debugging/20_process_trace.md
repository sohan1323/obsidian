
---
Attach to an existing process:

```
sudo strace -p PID
```

This lets you observe system calls made by the process.

Stop tracing with:

```
Ctrl+C
```

Attaching to a process may require appropriate permissions.



# `strace` Important Options

|Option|Purpose|
|---|---|
|`-p PID`|Attach to process|
|`-f`|Follow child processes|
|`-o FILE`|Write trace to file|
|`-e trace=...`|Select syscall classes|
|`-c`|Summarize system calls|
|`-T`|Show syscall time|
|`-t`|Show timestamps|
|`-tt`|More precise timestamps|

Example:

```
strace -c ls
```

Shows a syscall summary.


# Trace Specific System Calls

File-related calls:

```
strace -e trace=file command
```

Network-related:

```
strace -e trace=network command
```

Process-related:

```
strace -e trace=process command
```

Memory-related:

```
strace -e trace=memory command
```



# Practical `strace` Example

Suppose:

```
cat test.txt
```

Trace file operations:

```
strace -e trace=file cat test.txt
```

You can observe calls related to locating/opening the file.

This is useful when troubleshooting:

```
"Why can't this program find/open a file?"
```


# `strace -f`

Follow child processes:

```
strace -f ./script.sh
```

Useful when:

```
parent process
    ↓
fork/exec
    ↓
child process
```

Without `-f`, tracing may not follow all child activity.