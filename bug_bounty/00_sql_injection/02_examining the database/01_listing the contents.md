
---
### Listing Database Contents

To examine the database structure, you need to identify the **tables** and **columns** available in the database.

#### Non-Oracle databases

Most databases provide the `information_schema` views.

**List tables:**

```
SELECT * FROM information_schema.tables;
```

Important column:

```
TABLE_NAME
```

Example:

```
Products
Users
Feedback
```

**List columns of a specific table:**

```
SELECT *
FROM information_schema.columns
WHERE table_name = 'Users';
```

Important information returned:

```
COLUMN_NAME
DATA_TYPE
```

Example:

```
UserId    int
Username  varchar
Password  varchar
```

---

### Oracle

Oracle does not use `information_schema` in the same way.

**List tables:**

```
SELECT * FROM all_tables;
```

**List columns:**

```
SELECT *
FROM all_tab_columns
WHERE table_name = 'USERS';
```

### Comparison

|Purpose|Non-Oracle|Oracle|
|---|---|---|
|List tables|`information_schema.tables`|`all_tables`|
|List columns|`information_schema.columns`|`all_tab_columns`|
|Table name filter|`table_name = 'Users'`|`table_name = 'USERS'`|

The main concept is: **enumerate tables → identify interesting tables → enumerate their columns → determine what data they contain.**
