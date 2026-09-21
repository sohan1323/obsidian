
---
# What is Linux?

**Linux is an open-source operating system kernel** that manages the communication between computer hardware and software.
Linux was originally created by **Linus Torvalds in 1991** as a Unix-like kernel.


# What is the shell?

A **shell** is a program that allows you to interact with the operating system through commands.


# Linux architecture

![[Pasted image 20260921091326.png]]


# Linux Kernel vs GNU Utilities

### 1. Linux Kernel

The **Linux kernel** is the core of the operating system. It directly manages hardware and provides essential system services to programs.

Main responsibilities:

- **Process management** — creates, schedules, and terminates processes.
- **Memory management** — manages RAM and virtual memory.
- **File system management** — provides access to files and storage.
- **Device management** — communicates with hardware through drivers.
- **Networking** — manages network interfaces and network protocols.
- **Security and permissions** — enforces users, groups, permissions, capabilities, etc.
- **System calls** — provides an interface through which applications request kernel services.

### 2. GNU Utilities

**GNU utilities** are user-space programs that provide common commands for interacting with and managing the system.

Examples:

```
ls
cp
mv
rm
cat
chmod
chown
```


# Linux Distros

![[Pasted image 20260921094351.png]]


# Shell vs Terminal

### 1. Terminal

A **terminal** is the interface through which you interact with a command-line environment.
Modern Linux systems usually use a **terminal emulator**, which is a graphical application that provides a terminal window.

Examples:
- GNOME Terminal
- Konsole
- XTerm
- Tilix

### 2. Shell

A **shell** is a program that interprets the commands you type and executes them.

Common Linux shells:
- **Bash** — Bourne Again Shell
- Zsh
- Fish
- Dash
- Ksh

For example, when you type:

```
ls -la
```

the shell:

1. Reads the command.
2. Interprets it.
3. Finds the `ls` program.
4. Executes it.
5. Displays the result.



# TTY / PTY

**TTY** and **PTY** are mechanisms Linux uses to provide terminal interfaces for interacting with processes such as shells.

### 1. TTY

**TTY** originally comes from **Teletypewriter**.

In Linux, a TTY is a **terminal device** through which a user can interact with a shell or another terminal-based program.

You can see your current terminal with:

```
tty
```

Example:

```
/dev/pts/0
```

Linux also provides virtual terminals such as:

```
/dev/tty1
/dev/tty2
/dev/tty3
```

You can commonly switch between virtual consoles using:

```
Ctrl + Alt + F3
```

and return to the graphical environment using the appropriate function-key combination for your desktop/session.


### 2. PTY

**PTY** stands for **Pseudo-Terminal**.

A PTY is a **software-based terminal** that behaves like a real terminal.

It has two ends:

```
┌──────────────┐
│ PTY Master   │
└──────┬───────┘
       │
       │
┌──────▼───────┐
│ PTY Slave    │
└──────────────┘
```

The **master** is controlled by a program such as a terminal emulator or SSH server.

The **slave** behaves like a terminal device to the shell.


### 3. Terminal Emulator and PTY

When you open a graphical terminal such as GNOME Terminal:

```
GNOME Terminal
      │
      ↓
   PTY master
      │
      ↓
   PTY slave
      │
      ↓
     Bash
```

Bash believes it is communicating with a normal terminal, even though the terminal is actually implemented in software.

This is why you may see:

```
tty
```

return:

```
/dev/pts/0
```

`/dev/pts/` generally contains **pseudo-terminal slave devices**.



### 4. SSH and PTY

PTYs are also important with SSH.

When you connect interactively:

```
ssh user@server
```

SSH can allocate a pseudo-terminal:

```
Local terminal
      ↓
SSH client
      ↓
Network
      ↓
SSH server
      ↓
PTY
      ↓
Bash
```

This allows the remote shell to behave like an interactive terminal.



# Root User

The **root user** is the special administrative user in Linux with **UID 0**.
Root has very high privileges and can perform operations that normal users are not allowed to perform.

You can check it with:

```bash
id root
```

Typical output:

```
uid=0(root) gid=0(root) groups=0(root)
```

Root can generally:

- Read, modify, and delete system files
- Create or delete users
- Change file ownership and permissions
- Start, stop, and configure system services
- Modify system configuration
- Access hardware and devices
- Change networking configuration
- Terminate processes belonging to other users
- Install and remove system software

A root shell is commonly represented by a `#` prompt:

```
root@kali:~#
```

A normal user's prompt commonly uses `$`:

```
user@kali:~$
```

## `sudo`

Instead of logging in directly as root, Linux commonly allows authorized users to execute individual commands with elevated privileges using:

```
sudo command
```


# Root vs `sudo su` vs `sudo` vs Normal User vs Guest

These terms represent **different user/privilege situations**. Also, `sudo` and `sudo su` are **commands**, not types of users.

| Term            | What it is                                                     | Privilege level           | Typical use                      |
| --------------- | -------------------------------------------------------------- | ------------------------- | -------------------------------- |
| **Normal user** | Regular Linux account                                          | Limited                   | Daily work                       |
| **Guest**       | Restricted account/session                                     | Very limited              | Temporary/basic access           |
| **Root**        | Special administrative account, UID 0                          | Highest                   | System administration            |
| **`sudo`**      | Command for executing another command with elevated privileges | Elevated for that command | Administrative tasks             |
| **`sudo su`**   | Command that starts a shell as root                            | Root shell                | Multiple administrative commands |



# Linux Processes

A **process** is a **running instance of a program**.
Ex: Firefox program is loaded into memory and starts executing. That running instance is a **process**.

A process generally has:

- **PID** — Process ID
- **PPID** — Parent Process ID
- Process state
- CPU/register context
- Memory/address space
- Open file descriptors
- Environment variables
- User/group identity
- Security credentials

### 1. PID

**PID = Process ID**

Every running process is assigned a unique process ID.
You can see your current shell's PID:

```
echo $$
```

### 2. PPID

**PPID = Parent Process ID**

Processes can create other processes.
You can see the parent process using:

```bash
ps -o pid,ppid,cmd
```

### 3. Process States

Linux processes can exist in different states.

Common states include:

|State|Meaning|
|---|---|
|`R`|Running or runnable|
|`S`|Interruptible sleep|
|`D`|Uninterruptible sleep|
|`T`|Stopped|
|`Z`|Zombie|

You can see the state with:

```bash
ps aux
```

##### Zombie Process

A **zombie** is a process that has finished execution but still has an entry in the process table because its parent hasn't yet collected its exit status.





# System Calls

A **system call** is the controlled interface that allows a **user-space program to request a service from the Linux kernel**.
User-space programs cannot directly perform privileged operations such as accessing hardware or managing kernel resources. They use system calls to ask the kernel to perform those operations.

#### Common Linux System Calls

#### `open()`

Opens a file.

```bash
open("file.txt", O_RDONLY);
```

#### `read()`

Reads data from a file or file descriptor.

```bash
read(fd, buffer, size);
```

#### `write()`

Writes data.

```
write(fd, buffer, size);
```

#### `close()`

Closes a file descriptor.

```
close(fd);
```

#### `fork()`

Creates a new process.

```
fork();
```

#### `execve()`

Replaces the current process image with another program.

```
execve("/bin/ls", ...);
```

#### `wait()`

Allows a parent process to wait for a child process.

#### `exit()`

Terminates a process.


Linux provides `strace` for tracing system calls made by a program.

Example:

```bash
strace ls
```

You may see calls such as:

```
execve(...)
openat(...)
read(...)
write(...)
close(...)
```


# Daemons

A **daemon** is a **background process that runs without direct user interaction and provides a service or performs a system task**.

##### Examples

##### `sshd`

Provides the SSH server.

```
sshd → accepts SSH connections
```

##### `cron`

Runs scheduled tasks.

```
cron → checks scheduled jobs → executes them
```

##### `systemd`

The system and service manager on many modern Linux distributions.

It starts and manages many system services.

##### `NetworkManager`

Manages network connections and interfaces on systems where it is enabled.


### Daemon vs Normal Process

Process
  │
  ├── Interactive process
  │     └── directly associated with user activity
  │
  └── Daemon
        └── background service


A daemon typically:

- Runs in the background
- Provides a service
- Doesn't require continuous user interaction
- May start automatically during boot
- Often continues running while users log in and out


## Daemon vs Service

These terms are closely related but aren't exactly identical.

**Daemon** refers primarily to the **background process** providing functionality.

**Service** refers more broadly to the **functionality being provided** and, with systems such as `systemd`, also to the managed service unit.

For example:

```
SSH service
    ↓
sshd daemon
    ↓
Runs as a background process
```



# Environment Variables

**Environment variables** are **key-value pairs maintained by the operating system/shell that store information used by processes and programs during execution.**

They provide configuration and contextual information to programs without requiring that information to be hard-coded into the program.

Example:

```bash
echo $HOME
```

Output:

```
/home/user
```


## Common Environment Variables

##### `HOME`

User's home directory.

```bash
echo $HOME
```

Example:

```
/home/sohan
```

##### `USER`

Current username.

```bash
echo $USER
```

##### `SHELL`

Default/login shell.

```bash
echo $SHELL
```

Example:

```
/bin/bash
```

##### `PATH`

Directories where the shell searches for executable programs.

```bash
echo $PATH
```

Example:

```
/usr/local/bin:/usr/bin:/bin
```

##### `PWD`

Current working directory.

```bash
echo $PWD
```

##### `LANG`

Locale/language configuration.

```bash
echo $LANG
```


## Shell Variable vs Environment Variable

A normal shell variable:

```
name="Alex"
```

is available to the current shell.

To make it available to child processes, export it:

```
export name="Alex"
```

Now `name` becomes an **environment variable**.

```
Shell
 │
 ├── Variable
 │
 └── export
       ↓
   Environment variable
       ↓
   Child processes
```


## Viewing Environment Variables

Use:

```
env
```

or:

```
printenv
```

To view a specific variable:

```
printenv HOME
```


## Setting and Removing Variables

Set for the current shell:

```bash
MY_VAR="hello"
```

Export it:

```bash
export MY_VAR="hello"
```

Remove it:

```bash
unset MY_VAR
```
