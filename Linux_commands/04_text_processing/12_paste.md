
---
**Purpose:** Combine corresponding lines from files.

### Syntax

```
paste [OPTIONS] FILE1 FILE2
```

Suppose `names.txt`:

```
Alice
Bob
Charlie
```

and `ages.txt`:

```
20
21
22
```

Run:

```
paste names.txt ages.txt
```

Output:

```
Alice   20
Bob     21
Charlie 22
```

### Important options

|Option|Meaning|
|---|---|
|`-d DELIMITER`|Specify delimiter|
|`-s`|Combine lines sequentially|

Example:

```
paste -d ':' names.txt ages.txt
```

Output:

```
Alice:20
Bob:21
Charlie:22
```