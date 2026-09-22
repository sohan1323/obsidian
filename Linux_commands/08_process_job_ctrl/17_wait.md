
---
**Purpose:** Wait for background processes to finish.

### Syntax

```
wait [PID | JOB_ID]
```

Example:

```
./task.sh &
PID=$!

wait $PID
echo "Task finished"
```

`$!` contains the PID of the most recently started background process.

### Wait for a job

```
wait %1
```

### Practical shell scripting use

Run multiple tasks:

```
task1 &
task2 &
task3 &

wait

echo "All tasks completed"
```

---

# Important Job-Control Shortcuts

These aren't commands, but you must know them.

|Shortcut|Meaning|
|---|---|
|`Ctrl+C`|Send SIGINT to foreground process|
|`Ctrl+Z`|Suspend foreground process|
|`Ctrl+D`|EOF / close shell input|
|`Ctrl+\`|Send SIGQUIT|

Example:

```
ping 8.8.8.8
```

Press:

```
Ctrl+C
```

The ping process receives an interrupt and normally terminates.

---

# Process Relationships

Suppose:

```
bash
 └── python
      └── child process
```

You can investigate using:

```
pstree -p
```

Find Python:

```
pgrep -a python
```

Get detailed information:

```
ps -p PID -f
```

Terminate gracefully:

```
kill PID
```

If necessary:

```
kill -9 PID
```

---

# Important Process Information

For a process:

```
ps -p 1234 -f
```

You can inspect its `/proc` directory:

```
ls -la /proc/1234
```

Command line:

```
cat /proc/1234/cmdline
```

Environment:

```
cat /proc/1234/environ
```

Usually easier to read:

```
tr '\0' '\n' < /proc/1234/environ
```

Executable:

```
readlink -f /proc/1234/exe
```

Current working directory:

```
readlink -f /proc/1234/cwd
```

These `/proc` techniques become particularly useful during Linux process and privilege-escalation enumeration.

---

# Common Process Workflow

### Find high CPU processes

```
top
```

or:

```
ps aux --sort=-%cpu | head
```

### Find high memory processes

```
ps aux --sort=-%mem | head
```

### Find SSH processes

```
pgrep -a ssh
```

### Find a process

```
pgrep -a nginx
```

### Inspect it

```
ps -p PID -f
```

### View its process tree

```
pstree -p PID
```

### Terminate normally

```
kill PID
```

### Force if necessary

```
kill -9 PID
```