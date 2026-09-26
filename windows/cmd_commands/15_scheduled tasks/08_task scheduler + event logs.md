
---
Task Scheduler activity can also be investigated through Event Logs.

Find Task Scheduler channels:

```
wevtutil el | findstr /i "TaskScheduler"
```

A common channel is:

```
Microsoft-Windows-TaskScheduler/Operational
```

Query:

```
wevtutil qe Microsoft-Windows-TaskScheduler/Operational /c:20 /rd:true /f:text
```

This can help correlate:

```
Task trigger
    ↓
Task execution
    ↓
Task result
```