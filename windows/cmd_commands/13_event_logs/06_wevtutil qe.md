
---
`qe` = **Query Events**

This is the most important `wevtutil` operation.

### Basic syntax

```
wevtutil qe LogName
```

Example:

```
wevtutil qe System
```

This can produce a large amount of output.


# `/f`

Controls output format.

### Text

```
wevtutil qe System /f:text
```

### XML

```
wevtutil qe System /f:xml
```

XML is particularly useful when you need structured event information.


# `/c`

Limits the number of events returned.

```
wevtutil qe System /c:10
```

Returns approximately the most recent 10 matching events.

Example:

```
wevtutil qe Application /c:20 /f:text
```


# `/rd`

Controls reading direction.

### Newest first

```
wevtutil qe System /rd:true
```

### Oldest first

```
wevtutil qe System /rd:false
```

A useful combination:

```
wevtutil qe System /c:20 /rd:true /f:text
```


# `/q`

Applies an XPath query.

This is one of the most powerful features of `wevtutil`.

### Query a specific Event ID

```
wevtutil qe Security /q:"*[System[(EventID=4624)]]"
```

This searches for Security events with Event ID `4624`.