
---
  

# Blind SQL Injection in TrackingId Cookie allows Server-Side Query Delays

## 1. Executive Summary

A blind SQL injection vulnerability was identified in the `TrackingId` cookie, allowing an attacker to inject PostgreSQL SQL expressions into a database query. By injecting the `pg_sleep()` function, the attacker can intentionally delay the server's response, confirming that SQL injection is possible even when the application does not return database output or errors.

## 2. Vulnerability Details

- **Vulnerability Type:** Blind SQL Injection — Time-Based
    
- **Target Endpoint/URL:** Shop front page `/`
    
- **Affected Parameter:** `TrackingId` cookie
    
- **Database:** PostgreSQL
    
- **Authentication Level Required:** Unauthenticated
    

## 3. Steps to Reproduce (STR)

1. Open the target shop application and visit the front page.
    
2. Open **Burp Suite** and navigate to **Proxy → HTTP history**.
    
3. Locate the request for the front page containing the `TrackingId` cookie.
    
4. Send the request to **Repeater** for easier modification.
    
5. Modify the `TrackingId` cookie to:
    

```
TrackingId=x'||pg_sleep(10)--
```

6. Send the modified request.
    
7. Observe the response time.
    
8. The application takes approximately **10 seconds** to respond.
    
9. This confirms that the injected SQL expression was executed by the backend database.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

**Injected request:**

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=x'||pg_sleep(10)--
```

The important payload is:

```
x'||pg_sleep(10)--
```

The payload works by:

- `x'` — closes the existing SQL string.
    
- `||` — PostgreSQL string concatenation operator.
    
- `pg_sleep(10)` — instructs PostgreSQL to pause execution for 10 seconds.
    
- `--` — comments out the remainder of the original SQL statement.
    

**Observed behavior:**

```
Normal request      → Immediate response
Injected request   → ~10 second delay
```

The predictable delay demonstrates that the SQL expression was executed server-side.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

### Technical Impact

An attacker can exploit the vulnerable `TrackingId` cookie to inject SQL expressions into the backend database query. The demonstrated payload enables controlled server-side delays, confirming a time-based blind SQL injection vulnerability.

Because blind SQL injection does not require the application to directly return database results, an attacker may potentially use conditional time delays to infer sensitive database information character by character.

### Business Impact

Successful exploitation could potentially allow an attacker to extract sensitive database information, depending on the privileges of the database account used by the application. This could expose credentials, user information, application data, or other sensitive records and may lead to further compromise.

## 6. Remediation & References

### Suggested Fix

1. Use **parameterized queries / prepared statements** instead of dynamically constructing SQL queries with user-controlled input.
    
2. Treat cookie values such as `TrackingId` as untrusted input.
    
3. Avoid concatenating user-controlled values directly into SQL statements.
    
4. Apply the principle of **least privilege** to the application's database account.
    
5. Implement appropriate input validation as an additional defense, but do not rely on it as the primary SQL injection defense.
    
6. Monitor unusual database execution times and repeated requests that attempt to trigger database delays.
    

### References

- OWASP Top 10 — A03: Injection
    
- OWASP SQL Injection Prevention Cheat Sheet
    
- CWE-89 — Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
    
- PortSwigger Web Security Academy — Blind SQL Injection