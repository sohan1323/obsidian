
---
Displays currently running processes.

### Syntax

```
tasklist [/v] [/fo format] [/fi filter] [/m [module]] [/svc] [/nh] [/fi filter]
```

### Basic

```
tasklist
```

Example output:

```
Image Name                     PID Session Name        Mem Usage
========================= ======== ================ ============
System Idle Process              0 Services               8 K
System                           4 Services             200 K
explorer.exe                  4820 Console           120,000 K
chrome.exe                    7124 Console           450,000 K
```

Important fields:

|Field|Meaning|
|---|---|
|`Image Name`|Process executable|
|`PID`|Process ID|
|`Session Name`|Session containing process|
|`Session#`|Session ID|
|`Mem Usage`|Memory usage|

---

## `/v` — verbose

```
tasklist /v
```

Displays additional information such as:

- username
- CPU time
- window title
- session information

Useful when investigating processes.

---

## `/fo` — output format

```
tasklist /fo table
```

Formats:

```
TABLE
LIST
CSV
```

Example:

```
tasklist /fo list
```

Displays each process as a detailed list.

```
tasklist /fo csv
```

Useful when importing process information into another tool.

---

## `/fi` — filter

One of the most useful options.

### Find a specific process

```
tasklist /fi "imagename eq chrome.exe"
```

### Find by PID

```
tasklist /fi "pid eq 4820"
```

### Find processes using lots of memory

```
tasklist /fi "memusage gt 100000"
```

### Find processes running under a user

```
tasklist /fi "username eq Sohan"
```

### Common filter operators

|Operator|Meaning|
|---|---|
|`eq`|Equal|
|`ne`|Not equal|
|`gt`|Greater than|
|`lt`|Less than|
|`ge`|Greater/equal|
|`le`|Less/equal|

---

## `/m`

Displays processes associated with a DLL/module.

```
tasklist /m
```

Specific module:

```
tasklist /m kernel32.dll
```

This can be useful during Windows troubleshooting and process investigation.

---

## `/svc`

Shows services hosted by each process.

```
tasklist /svc
```

This is particularly useful because Windows frequently hosts multiple services inside processes such as:

```
svchost.exe
```

You can investigate:

```
tasklist /svc /fi "imagename eq svchost.exe"
```

---

## `/nh`

Suppresses column headers.

```
tasklist /nh
```

Useful for scripting.