
---
For authorized Windows administration or security assessment:

### 1. List services

```
sc query
```

### 2. Find a specific service

```
sc query Spooler
```

### 3. Get PID

```
sc queryex Spooler
```

### 4. Inspect configuration

```
sc qc Spooler
```

### 5. Inspect dependencies

```
sc enumdepend Spooler
```

### 6. Inspect permissions

```
sc sdshow Spooler
```

### 7. Identify the process

```
tasklist /fi "PID eq 1234"
```

This gives you the chain:

```
Service
   ↓
Service configuration
   ↓
Service account
   ↓
Binary path
   ↓
PID
   ↓
Process
```