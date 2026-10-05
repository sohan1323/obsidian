
---
### SQLi Example — Examining the Database

SQL injection can sometimes be used to **discover information about the database itself**, such as:

- Database type and version
- Database name
- Tables
- Columns
- Database users
- Database schema/structure

For example, an injectable application might allow an attacker to determine the database version using a database-specific query:

```
SELECT version();
```

The attacker can then investigate the database's metadata/schema to identify available tables and columns.

For example, in databases that provide an information schema:

```
SELECT table_name
FROM information_schema.tables;
```

This can reveal table names such as:

```
users
products
orders
payments
```

The attacker can then identify the columns within interesting tables:

```
SELECT column_name
FROM information_schema.columns
WHERE table_name = 'users';
```

Which might reveal:

```
id
username
email
password
```

**Impact:** SQL injection can allow an attacker to **enumerate the database structure**, making it easier to identify and subsequently access sensitive data.