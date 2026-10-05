
---
**Windows NT architecture** is the design of the Windows operating system that defines how hardware, the kernel, system services, applications, and users interact.

Modern Windows versions such as **Windows 10 and Windows 11** are based on the Windows NT architecture.

The architecture is broadly divided into:

```
┌──────────────────────────────────────┐
│             User Mode                │
│                                      │
│  Applications                        │
│  Windows Subsystems / APIs           │
│  Service Processes                   │
│                                      │
├────────────── System Call Boundary ──┤
│             Kernel Mode              │
│                                      │
│  Executive                          │
│  Kernel                              │
│  Device Drivers                      │
│  HAL                                 │
│                                      │
├──────────────────────────────────────┤
│             Hardware                 │
└──────────────────────────────────────┘
```

---

# 1. Hardware

At the bottom is the physical hardware:

- CPU
- RAM
- Disk
- Network adapter
- Keyboard/mouse
- Display
- Other devices

Applications **do not normally communicate directly with hardware**.

They request services from Windows, which eventually interact with the hardware through kernel-mode components and drivers.

---

# 2. Hardware Abstraction Layer — HAL

**HAL (Hardware Abstraction Layer)** provides an abstraction between Windows and hardware-specific details.

```
Windows NT
    ↓
   HAL
    ↓
Hardware
```

Its purpose is to hide many hardware-specific implementation details from the rest of the operating system.

For example, different hardware platforms may implement interrupts or other low-level mechanisms differently. HAL provides a standardized interface that Windows components can use.

---

# 3. Kernel

The **Windows NT kernel** is the core of the operating system.

It handles fundamental low-level operations such as:

- Thread scheduling
- Interrupt handling
- Processor synchronization
- Low-level memory management
- Hardware interaction

The kernel is highly privileged and executes in **kernel mode**.

It should be distinguished from the **Executive**.

```
Kernel
  ↓
Low-level core OS mechanisms

Executive
  ↓
Higher-level OS management services
```

---

# 4. Executive

The **Executive** is a collection of kernel-mode operating-system components that provide major system-management functionality.

Important Executive components include:

### Memory Manager

Manages:

- Virtual memory
- Physical memory
- Memory mappings
- Paging

---

### Process Manager

Manages:

- Processes
- Threads
- Process creation
- Thread creation and termination

---

### I/O Manager

Controls the Windows I/O subsystem.

It provides a common framework for operations involving:

- Files
- Devices
- Network I/O
- Drivers

For example:

```
Application
     ↓
Windows API
     ↓
I/O Manager
     ↓
File-system driver
     ↓
Disk
```

---

### Object Manager

Windows represents many operating-system resources as **objects**.

Examples include:

- Processes
- Threads
- Files
- Events
- Mutexes
- Semaphores
- Tokens
- Sections

The Object Manager provides mechanisms for creating, managing, naming, and accessing these objects.

---

### Security Reference Monitor

Responsible for enforcing Windows security rules.

It works with mechanisms such as:

- Access tokens
- Security identifiers (SIDs)
- Security descriptors
- Access control lists (ACLs)

For example:

```
User
 ↓
Access Token
 ↓
Request resource
 ↓
Security Reference Monitor
 ↓
ACL / Security Descriptor
 ↓
Allow or Deny
```

This component is particularly important for understanding **Windows permissions and privilege**.

---

### Configuration Manager

Manages the Windows **Registry** at the kernel level.

The Registry contains configuration information used by Windows and applications.

---

### Plug and Play Manager

Manages hardware detection and device configuration.

For example:

```
USB device connected
        ↓
Plug and Play Manager
        ↓
Identify device
        ↓
Find/configure driver
        ↓
Device becomes available
```

---

### Power Manager

Manages system power-related operations such as:

- Sleep
- Hibernate
- Shutdown
- Power-state transitions

---

# 5. Device Drivers

**Device drivers** are kernel-mode components that allow Windows to communicate with hardware and certain software-based devices.

Examples:

```
Network card
    ↓
Network driver

Disk
    ↓
Storage driver

GPU
    ↓
Graphics driver
```

Drivers operate with high privileges, so a faulty or malicious kernel driver can have significant security consequences.

---

# 6. User Mode

Applications normally run in **user mode**.

Examples:

- Chrome
- Notepad
- PowerShell
- Windows Explorer
- Python programs
- Other applications

User-mode applications have restricted access to system resources.

For example:

```
Application
     ↓
Cannot directly access arbitrary kernel memory
     ↓
Requests OS service
     ↓
System call
     ↓
Kernel mode
```

This separation helps prevent one ordinary application from directly interfering with the operating system or other processes.

---

# 7. Windows Subsystems

Windows provides APIs and subsystem components that allow applications to interact with the operating system.

The most important one is the **Windows subsystem**, through which Windows applications use APIs such as:

```
CreateProcess()
CreateFile()
ReadFile()
WriteFile()
VirtualAlloc()
RegOpenKeyEx()
```

Applications normally use higher-level APIs rather than directly invoking low-level kernel functionality.

---

# 8. System Calls

A **system call** is the controlled transition from user mode to kernel mode when a user-mode program requests an operating-system service.

Simplified flow:

```
User Mode
────────────────────

Application
     ↓
Windows API
     ↓
System-call interface

════════════════════
  User → Kernel
════════════════════

Kernel Mode
     ↓
Executive / Kernel
     ↓
Hardware / Driver
```

For example, an application wants to read a file:

```
Application
     ↓
ReadFile()
     ↓
System call
     ↓
I/O Manager
     ↓
File-system driver
     ↓
Storage driver
     ↓
Disk
```

---

# Overall Windows NT Architecture

```
                 USER MODE
┌─────────────────────────────────────────┐
│ Applications                            │
│                                         │
│ PowerShell │ Explorer │ Applications    │
├─────────────────────────────────────────┤
│ Windows APIs / User-mode subsystems     │
│ Services / Runtime components           │
└───────────────────┬─────────────────────┘
                    │
              System Calls
                    │
════════════════════▼════════════════════
                 KERNEL MODE
┌─────────────────────────────────────────┐
│ Executive                              │
│                                         │
│ Object Manager                          │
│ Process Manager                         │
│ Memory Manager                          │
│ I/O Manager                             │
│ Security Reference Monitor              │
│ Configuration Manager                   │
│ Plug and Play Manager                   │
│ Power Manager                            │
├─────────────────────────────────────────┤
│ Kernel                                  │
├─────────────────────────────────────────┤
│ Device Drivers                          │
├─────────────────────────────────────────┤
│ HAL                                     │
└───────────────────┬─────────────────────┘
                    │
                    ▼
                 HARDWARE
```