
---
Displays the **service configuration**.

### Syntax

```
sc qc ServiceName
```

Example:

```
sc qc Spooler
```

Typical output contains:

```
SERVICE_NAME
TYPE
START_TYPE
ERROR_CONTROL
BINARY_PATH_NAME
LOAD_ORDER_GROUP
TAG
DISPLAY_NAME
DEPENDENCIES
SERVICE_START_NAME
```

### Important fields

|Field|Meaning|
|---|---|
|`SERVICE_NAME`|Internal service name|
|`DISPLAY_NAME`|Human-readable name|
|`START_TYPE`|How the service starts|
|`BINARY_PATH_NAME`|Executable/service command|
|`DEPENDENCIES`|Services required|
|`SERVICE_START_NAME`|Account running the service|

For example:

```
sc qc Spooler
```

can reveal that the service runs under a particular Windows service account.