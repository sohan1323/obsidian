
---
`typeperf` collects performance-counter information from Windows.

### Basic

```
typeperf "\Processor(_Total)\% Processor Time"
```

Collect a limited number:

```
typeperf "\Processor(_Total)\% Processor Time" -sc 5
```

Here:

```
-sc 5
```

collects five samples.