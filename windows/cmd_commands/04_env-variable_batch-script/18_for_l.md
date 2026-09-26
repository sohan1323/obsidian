
---
Generates a numeric sequence.

### Syntax

```
for /l %variable in (start,step,end) do command
```

Example:

```
for /l %i in (1,1,5) do echo %i
```

Output:

```
1
2
3
4
5
```

Count by 2:

```
for /l %i in (0,2,10) do echo %i
```

Output:

```
0
2
4
6
8
10
```

Countdown:

```
for /l %i in (10,-1,1) do echo %i
```