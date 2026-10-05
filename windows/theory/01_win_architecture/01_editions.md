
---
## 1. Windows Home

**Windows Home** is the edition primarily designed for **personal/home users**.

### Purpose

Used for:

- Personal computers
- Gaming
- Browsing
- Office/productivity work
- General desktop use

### Key characteristics

Windows Home contains the standard Windows desktop features but has fewer advanced **enterprise management and administration** features.

Examples of features generally associated with higher editions rather than Home include:

- Domain Join
- Group Policy management
- Advanced enterprise management
- Some virtualization/security capabilities

### Typical user

```
Individual user
      ↓
Windows Home
      ↓
Personal PC / Laptop
```

---

# 2. Windows Pro

**Windows Pro** is designed for **professional users, developers, IT professionals, and small businesses**.

It includes everything normally needed for a standard desktop environment plus additional administration and security capabilities.

### Important features

#### Domain Join

A Pro machine can join an organization's **Active Directory domain**.

For example:

```
Windows 11 Pro
      ↓
Join
      ↓
CORP.LOCAL
      ↓
Domain-controlled computer
```

This is important in corporate environments.

---

#### Group Policy

Windows Pro supports **Group Policy** functionality for managing Windows settings.

For example, administrators can control:

- Password policies
- Windows security settings
- User permissions
- Software restrictions
- System configuration

---

#### BitLocker

Pro supports **BitLocker** drive encryption on supported hardware/configurations.

It can encrypt the Windows drive so that the data is protected if the physical disk is removed.

---

#### Hyper-V

Windows Pro supports **Hyper-V**, Microsoft's native virtualization platform, subject to hardware and Windows-version requirements.

It can be used to create virtual machines such as:

```
Windows Pro
     │
     └── Hyper-V
          ├── Windows VM
          ├── Linux VM
          └── Windows Server VM
```

---

#### Remote Desktop

Windows Pro can act as a **Remote Desktop host**, allowing another computer to remotely connect to it using Microsoft's Remote Desktop protocol.

---

### Typical users

```
Developer
IT Professional
Power User
Small Business
        ↓
    Windows Pro
```

For cybersecurity labs, **Windows Pro is particularly useful** because features such as domain connectivity, Group Policy, BitLocker, Hyper-V, and Remote Desktop are relevant to Windows administration and security testing.

---

# 3. Windows Enterprise

**Windows Enterprise** is designed primarily for **large organizations and enterprise environments**.

It builds on the capabilities of Pro and adds additional enterprise-focused security, management, and deployment functionality.

### Main purpose

Enterprise environments may have:

```
Thousands of computers
        ↓
Centralized management
        ↓
Security policies
        ↓
Application/device control
        ↓
Enterprise Windows
```

### Important capabilities

Enterprise editions provide additional capabilities around areas such as:

- Advanced security
- Enterprise device management
- Application control
- Deployment
- Identity management
- Organizational policy enforcement

Examples of technologies associated with Enterprise environments include:

- Microsoft Defender for Endpoint
- Windows Defender Application Control
- AppLocker
- Enterprise management capabilities
- Advanced deployment/servicing options

Availability and exact feature sets vary by Windows version and licensing channel.

### Enterprise vs Pro

A simplified comparison:

|Feature|Home|Pro|Enterprise|
|---|---|---|---|
|Normal Windows desktop|✅|✅|✅|
|Domain Join|❌|✅|✅|
|Group Policy|Limited|✅|✅|
|BitLocker|✅*|✅|✅|
|Hyper-V|❌|✅|✅|
|Remote Desktop host|❌|✅|✅|
|Enterprise security/management|Limited|Some|Extensive|
|Large organization deployment|❌|Limited|✅|

*BitLocker availability and functionality can vary by device and Windows version; Windows Home may provide **Device Encryption** on supported hardware rather than the full BitLocker management experience.

---

# 4. Windows Server

**Windows Server is different from Windows Home/Pro/Enterprise desktop editions.**

It is specifically designed to operate **servers and provide network services**.

Instead of primarily being a user's desktop operating system, Windows Server is intended to provide services to other computers and users.

### Example

```
             Windows Server
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
 Active Directory DNS      DHCP
        │
        ↓
   Windows Clients
```

### Common Windows Server roles

#### Active Directory Domain Services (AD DS)

Provides centralized identity and authentication.

```
             Domain Controller
                    │
             AD DS / Directory
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
     User 1       User 2       User 3
```

---

#### DNS Server

Resolves names to IP addresses within a network.

```
dc01.corp.local
       ↓
    IP address
```

---

#### DHCP Server

Automatically provides network configuration to clients.

```
Windows Client
      ↓
DHCP Request
      ↓
Windows Server
      ↓
IP + Gateway + DNS
```

---

#### File Server

Provides centralized network file storage.

```
Client 1 ──┐
Client 2 ──┼──> Windows Server
Client 3 ──┘        │
                    ↓
              Shared folders
```

---

#### IIS

**Internet Information Services (IIS)** is Microsoft's web server platform.

It can host:

- Websites
- Web applications
- APIs
- ASP.NET applications