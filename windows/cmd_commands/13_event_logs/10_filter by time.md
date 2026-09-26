
---
XPath can filter event timestamps.

For example, events after a specific UTC timestamp:

```
wevtutil qe System /q:"*[System[TimeCreated[@SystemTime>='2026-09-25T00:00:00.000Z']]]" /f:text
```

The exact timestamp must be formatted appropriately.