
---
Windows separates code execution into **User Mode** and **Kernel Mode** primarily to provide **security, isolation, and system stability**.

```
┌──────────────────────────────┐
│          USER MODE           │
│                              │
│  Applications                │
│  PowerShell                  │
│  Browser                     │
│  User processes              │
│                              │
│     Restricted access        │
└──────────────┬───────────────┘
               │
          System Call
               │
┌──────────────▼───────────────┐
│         KERNEL MODE          │
│                              │
│  Windows Kernel              │
│  Executive                   │
│  Device Drivers              │
│                              │
│     Privileged access        │
└──────────────┬───────────────┘
               │
               ▼
            Hardware
```

---

# 1. User Mode

**User mode** is the restricted execution environment where normal applications run.

Examples:

- Chrome
- Notepad
- PowerShell
- Windows Explorer
- Python programs
- Most Windows services

A user-mode process does **not have unrestricted access to the system**.

### Why?

Suppose a normal application could directly modify:

- Kernel memory
- Another process's protected memory
- Hardware
- Critical OS structures

A buggy or malicious application could crash or compromise the entire operating system.

Therefore Windows isolates applications from the kernel.

---

## User-mode process

Each user-mode process normally gets its own **virtual address space**.

For example:

```
Process A
┌──────────────────┐
│ Its memory       │
└──────────────────┘

Process B
┌──────────────────┐
│ Its memory       │
└──────────────────┘
```

Process A cannot simply access Process B's memory.

Access to protected resources must go through Windows mechanisms.

---

# 2. Kernel Mode

**Kernel mode** is the highly privileged execution environment used by the Windows kernel and other trusted kernel-mode components.

Examples include:

- Windows kernel
- Windows Executive components
- Device drivers

Kernel-mode code has access to critical system resources.

It can interact with:

- Hardware
- Kernel memory
- Physical memory through appropriate mechanisms
- Device drivers
- System-wide resources
- Other protected operating-system structures

---

# 3. How User Mode Communicates With Kernel Mode

A user-mode application cannot normally perform privileged operations directly.

Instead, it requests the operating system to perform the operation.

Example:

```
Application
     │
     │ CreateFile()
     ▼
Windows API
     │
     ▼
System-call mechanism
     │
     ▼
Kernel Mode
     │
     ▼
I/O Manager
     │
     ▼
File-system / storage driver
     │
     ▼
Disk
```

The transition from user mode to kernel mode is controlled by the operating system.

---

# 4. Privilege Difference

The fundamental difference is **privilege level**.

|                                       | User Mode               | Kernel Mode          |
| ------------------------------------- | ----------------------- | -------------------- |
| Privilege                             | Restricted              | Highly privileged    |
| Applications                          | Yes                     | No                   |
| Kernel access                         | No                      | Yes                  |
| Hardware access                       | Indirect                | Direct/privileged    |
| Access to kernel memory               | Restricted              | Yes                  |
| Can access protected system resources | Through OS interfaces   | Yes                  |
| Failure impact                        | Usually affects process | Can affect entire OS |

---

# 5. What Happens If User-Mode Code Crashes?

Suppose Chrome crashes:

```
Chrome
   ↓
Crash
   ↓
Chrome process terminates
   ↓
Windows continues running
```

Normally, other applications and Windows itself continue operating.

---

# 6. What Happens If Kernel-Mode Code Crashes?

Suppose a kernel driver has a serious error:

```
Kernel driver
      ↓
Critical failure
      ↓
Windows detects kernel failure
      ↓
Bug Check
      ↓
Blue Screen of Death (BSOD)
```

This is because kernel-mode code operates at a much higher privilege level.

---

# 7. Security Importance

The boundary between user mode and kernel mode is an important **security boundary**.

A normal application:

```
User Mode
    ↓
Limited privileges
```

A kernel component:

```
Kernel Mode
    ↓
Very high privileges
```

Therefore, vulnerabilities that allow an attacker to move from **user mode to kernel mode** can be extremely serious because they may allow execution with kernel-level privileges.

This is commonly referred to as **kernel-mode privilege escalation**.