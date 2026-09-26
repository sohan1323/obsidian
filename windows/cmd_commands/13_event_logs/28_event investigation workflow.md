
---
For a Windows security investigation:

### 1. List logs

```
wevtutil el
```

### 2. Inspect Security configuration

```
wevtutil gl Security
```

### 3. Get recent security events

```
wevtutil qe Security /c:20 /rd:true /f:text
```

### 4. Check successful logons

```
wevtutil qe Security /q:"*[System[(EventID=4624)]]" /c:20 /rd:true /f:text
```

### 5. Check failed logons

```
wevtutil qe Security /q:"*[System[(EventID=4625)]]" /c:20 /rd:true /f:text
```

### 6. Check process creation

```
wevtutil qe Security /q:"*[System[(EventID=4688)]]" /c:20 /rd:true /f:text
```

### 7. Export evidence

```
wevtutil epl Security C:\Lab\Security.evtx
```