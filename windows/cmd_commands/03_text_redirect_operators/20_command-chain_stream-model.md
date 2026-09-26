
---
# Practical Command Chains

Now combine everything.

## Find IPv4 addresses

```
ipconfig /all | findstr /i "IPv4"
```

---

## Find listening ports

```
netstat -ano | findstr "LISTENING"
```

---

## Find a process

```
tasklist | findstr /i "chrome"
```

---

## Save network information

```
ipconfig /all > network.txt
```

---

## Save network information including errors

```
ipconfig /all > network.txt 2>&1
```

---

## Append another command's output

```
echo ===== Processes ===== >> system.txt
tasklist >> system.txt
```

---

## Run command and report success/failure

```
mkdir C:\CLI-Test && echo Created successfully || echo Creation failed
```

---

## Search recursively

```
findstr /s /i /n "password" C:\Lab\*.txt
```

This is a useful **authorized lab/security investigation** pattern.

---

# Stream Model

Remember this diagram:

```
             ┌───────────────┐
stdin  ─────►│               │
             │    COMMAND    │─────► stdout (1)
             │               │
             └───────────────┘
                      │
                      └────────────► stderr (2)
```

You can redirect them:

```
command > output.txt
```

```
command 2> errors.txt
```

```
command > output.txt 2>&1
```

And pipe stdout:

```
command1 | command2
```

This model will become very important when we reach **PowerShell pipelines**, where the concept is significantly more powerful because PowerShell passes **objects rather than plain text**.