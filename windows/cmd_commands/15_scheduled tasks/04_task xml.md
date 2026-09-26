
---
Task Scheduler tasks can be represented as XML.

Querying with:

```
schtasks /query /tn "LabTask" /xml
```

can provide an XML representation on supported Windows versions.

XML is useful for:

- Backups
- Task migration
- Automation
- Detailed configuration analysis

# XML Task Creation

You can create a task from an XML definition:

```
schtasks /create /tn "LabTask" /xml C:\Lab\LabTask.xml
```

This gives you much more control than the basic `/create` syntax.