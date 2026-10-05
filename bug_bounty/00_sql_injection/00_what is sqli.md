
---
What is SQL injection (SQLi)?
SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allow an attacker to view data that they are not normally able to retrieve. This might include data that belongs to other users, or any other data that the application can access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

These are the **main manual techniques for detecting SQL injection**:

1. **Single quote `'`**
    
    - Submit `'` into an input.
    - Look for SQL errors, unexpected behavior, or other anomalies.

2. **SQL syntax that preserves/changes the original value**
    
    - Send syntax that evaluates to the original value.
    - Then send syntax that evaluates to a different value.
    - Compare the application's responses.

3. **Boolean conditions**
    
    ```
    OR 1=1
    OR 1=2
    ```
    
    - `1=1` is always true.
    - `1=2` is always false.
    - A consistent difference between responses can indicate SQL injection.
4. **Time-delay payloads**
    
    - Send a payload designed to make the database deliberately delay its response.
    - A consistent delay can indicate that the input is being executed as SQL.

5. **OAST (Out-of-Band) payloads**
    
    - Send a payload that causes the database/server to make an external network interaction.
    - Monitor for that interaction.
    - An interaction can confirm that the input reached and was executed by the database.

### Common locations

| Query type / location    | Example                                              |
| ------------------------ | ---------------------------------------------------- |
| **SELECT – WHERE**       | `SELECT * FROM users WHERE id = '$input'`            |
| **UPDATE – values**      | `UPDATE users SET email = '$input' WHERE id = 1`     |
| **UPDATE – WHERE**       | `UPDATE users SET role = 'user' WHERE id = '$input'` |
| **INSERT – values**      | `INSERT INTO users (name) VALUES ('$input')`         |
| **SELECT – table name**  | `SELECT * FROM $input`                               |
| **SELECT – column name** | `SELECT $input FROM users`                           |
| **SELECT – ORDER BY**    | `SELECT * FROM users ORDER BY $input`                |


### Types of SQL Injection

1. **In-band SQL Injection**
    
    - Attacker uses the same channel to inject SQL and receive results.
    - Types:
        - **Error-based SQLi**
        - **UNION-based SQLi**

2. **Blind SQL Injection**
    
    - Application does not directly return database results.
    - Attacker infers information from application behavior.
    - Types:
        - **Boolean-based SQLi**
        - **Time-based SQLi**

3. **Out-of-band (OAST) SQL Injection**
    
    - Database/server sends data or triggers a network interaction through a separate channel.
    - Useful when neither direct output nor timing differences are available.

Warning
Take care when injecting the condition OR 1=1 into a SQL query. Even if it appears to be harmless in the context you're injecting into, it's common for applications to use data from a single request in multiple different queries. If your condition reaches an UPDATE or DELETE statement, for example, it can result in an accidental loss of data.