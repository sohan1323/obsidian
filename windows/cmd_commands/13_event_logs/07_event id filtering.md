
---
For example:

```
wevtutil qe Security /q:"*[System[(EventID=4625)]]" /rd:true /c:20 /f:text
```

This queries recent events with Event ID `4625`.

In Windows security auditing, common event IDs include:

|Event ID|General meaning|
|---|---|
|`4624`|Successful logon|
|`4625`|Failed logon|
|`4634`|Logoff|
|`4647`|User-initiated logoff|
|`4672`|Special privileges assigned to new logon|
|`4688`|New process created|
|`4697`|Service installed|
|`4720`|User account created|
|`4722`|User account enabled|
|`4725`|User account disabled|
|`4726`|User account deleted|
|`4732`|Member added to local security-enabled group|
|`4740`|User account locked out|
|`1102`|Security audit log cleared|

The exact events available depend on **Windows version and enabled audit policy**.