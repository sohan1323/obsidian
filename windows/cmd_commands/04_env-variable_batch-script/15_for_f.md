
---
`for /f` processes text, files, or command output.

This is one of the most powerful CMD scripting constructs.

### Read a file

```
for /f %i in (users.txt) do echo %i
```

Suppose:

```
users.txt
```

contains:

```
alice
bob
charlie
```

Output:

```
alice
bob
charlie
```

---

## Process command output

Use:

```
for /f %i in ('command') do echo %i
```

Example:

```
for /f %i in ('hostname') do echo Computer: %i
```

Another useful example:

```
for /f "tokens=*" %i in ('whoami') do echo User: %i
```

---

## `tokens`

Suppose:

```
users.txt
```

contains:

```
Alice Admin
Bob User
Charlie Guest
```

Then:

```
for /f "tokens=1" %a in (users.txt) do echo %a
```

gets the first token:

```
Alice
Bob
Charlie
```

Second token:

```
for /f "tokens=2" %a in (users.txt) do echo %a
```

gets:

```
Admin
User
Guest
```

Multiple tokens:

```
for /f "tokens=1,2" %a in (users.txt) do echo %a %b
```

---

## `delims`

Controls token separators.

```
for /f "tokens=1 delims=," %a in (data.txt) do echo %a
```

Useful for comma-separated data.