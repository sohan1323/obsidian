
---
### Examining the Database — Querying Database Type and Version

A successful SQL injection can sometimes be used to determine **which database management system (DBMS)** the application is using and its **version**.

Different databases provide different version-identification functions.

|Database|Version query|
|---|---|
|**MySQL**|`SELECT @@version`|
|**PostgreSQL**|`SELECT version()`|
|**Microsoft SQL Server**|`SELECT @@version`|
|**Oracle**|`SELECT banner FROM v$version`|
|**SQLite**|`SELECT sqlite_version()`|

For example, with PostgreSQL:

```
SELECT version();
```

might return information such as:

```
PostgreSQL 16.x ...
```

### Why this matters

Knowing the **DBMS and version** helps an attacker determine:

- Which SQL syntax is supported
- Which database-specific functions are available
- Which system tables/views can be queried
- Which SQLi techniques are applicable

The exact query syntax is **DBMS-specific**, so identifying the database type is often an important early step when examining a SQL injection vulnerability.