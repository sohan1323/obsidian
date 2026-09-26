
---
On a Windows server:

```
net session
```

Shows connected clients.

Then:

```
net file
```

Shows files opened through network sharing.

Then:

```
net share
```

Shows available shares.

So:

```
net share
    ↓
What is shared?

net session
    ↓
Who is connected?

net file
    ↓
What network files are open?
```