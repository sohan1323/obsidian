
---
**Purpose:** Join lines from two files based on a common field.

This is conceptually similar to a SQL `JOIN`.

### Syntax

```
join [OPTIONS] FILE1 FILE2
```

Suppose:

`users.txt`

```
1 Alice
2 Bob
3 Charlie
```

`departments.txt`

```
1 Security
2 Development
3 Networking
```

Run:

```
join users.txt departments.txt
```

Output:

```
1 Alice Security
2 Bob Development
3 Charlie Networking
```

### Important options

|Option|Meaning|
|---|---|
|`-1 FIELD`|Join using field from file 1|
|`-2 FIELD`|Join using field from file 2|
|`-t CHAR`|Field separator|
|`-a FILE`|Include unmatched lines|
|`-v FILE`|Show only unmatched lines|

### Practical note

By default, input files generally need to be sorted on the join field.