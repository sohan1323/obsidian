
---
These are useful to recognize during Windows security investigations:

|Event ID|General meaning|
|---|---|
|`4624`|Successful logon|
|`4625`|Failed logon|
|`4634`|Logoff|
|`4647`|User initiated logoff|
|`4672`|Special privileges assigned to new logon|
|`4688`|Process creation|
|`4697`|Service installed|
|`4720`|User created|
|`4722`|User enabled|
|`4725`|User disabled|
|`4726`|User deleted|
|`4732`|Member added to local security-enabled group|
|`4740`|Account locked out|
|`1102`|Security audit log cleared|

These IDs should be interpreted in context. Event availability and fields depend on the Windows version and configured auditing.