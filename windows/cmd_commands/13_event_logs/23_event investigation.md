
---
One of the most useful logs for Windows security analysis is:

```
Security
```

Check recent events:

```
wevtutil qe Security /c:20 /rd:true /f:text
```

Successful logons:

```
wevtutil qe Security /q:"*[System[(EventID=4624)]]" /c:20 /rd:true /f:text
```

Failed logons:

```
wevtutil qe Security /q:"*[System[(EventID=4625)]]" /c:20 /rd:true /f:text
```

Process creation:

```
wevtutil qe Security /q:"*[System[(EventID=4688)]]" /c:20 /rd:true /f:text
```

Account creation:

```
wevtutil qe Security /q:"*[System[(EventID=4720)]]" /c:20 /rd:true /f:text
```

Account lockout:

```
wevtutil qe Security /q:"*[System[(EventID=4740)]]" /c:20 /rd:true /f:text
```