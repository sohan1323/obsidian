
---
Displays network connections, listening ports, routing information, and statistics.

This is an **extremely important Windows security/networking command**.

### Syntax

```
netstat [-a] [-b] [-e] [-f] [-n] [-o] [-p protocol]
        [-q] [-r] [-s] [-t] [-x] [interval]
```

---

## Basic

```
netstat
```

Shows active connections.

---

## `-a`

Show all connections and listening ports:

```
netstat -a
```

---

## `-n`

Don't resolve names.

```
netstat -n
```

Shows numerical addresses/ports.

---

## `-o`

Show PID:

```
netstat -o
```

This is very useful.

Example:

```
TCP    0.0.0.0:443    0.0.0.0:0    LISTENING    1234
```

PID:

```
1234
```

Then:

```
tasklist /fi "pid eq 1234"
```

identifies the process.

---

## `-ano`

One of the most useful combinations:

```
netstat -ano
```

Means:

```
-a → all
-n → numerical
-o → owning PID
```

---

## Find listening ports

```
netstat -ano | findstr "LISTENING"
```

---

## Find a particular port

```
netstat -ano | findstr ":443"
```

---

## Find established connections

```
netstat -ano | findstr "ESTABLISHED"
```

---

## `-b`

Displays the executable responsible for each connection.

```
netstat -ab
```

This can require elevated privileges.

Because it can be expensive, use it selectively.

---

## `-f`

Display fully qualified domain names:

```
netstat -af
```

---

## `-r`

Display routing table:

```
netstat -r
```

Equivalent conceptually to:

```
route print
```

---

## `-e`

Ethernet statistics:

```
netstat -e
```

---

## `-s`

Protocol statistics:

```
netstat -s
```

You can query specific protocol statistics:

```
netstat -s -p tcp
```

---

## Interval

```
netstat -ano 5
```

Refreshes every 5 seconds until interrupted.

Stop with:

```
Ctrl+C
```