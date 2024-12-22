
---

### **MSFconsole Commands**

| **Command**                    | **Description**                                           |
| ------------------------------ | --------------------------------------------------------- |
| `show exploits`                | Display all exploits in the Framework.                    |
| `show payloads`                | Display all payloads in the Framework.                    |
| `show auxiliary`               | Display all auxiliary modules in the Framework.           |
| `search <name>`                | Search for exploits/modules by name.                      |
| `info`                         | Load detailed information about a module.                 |
| `use <name>`                   | Load a module (e.g., `use windows/smb/psexec`).           |
| `use <number>`                 | Load a module using its index number.                     |
| `set <option>`                 | Set a specific value (e.g., `LHOST`, `RHOST`).            |
| `setg <option>`                | Set a specific value globally.                            |
| `show options`                 | Display available options for a module.                   |
| `show targets`                 | Display supported platforms for an exploit.               |
| `set target <number>`          | Set a specific target index.                              |
| `set payload <payload>`        | Specify the payload to use.                               |
| `set payload <number>`         | Specify the payload using its index number.               |
| `show advanced`                | Display advanced options for a module.                    |
| `set autorunscript migrate -f` | Automatically migrate processes after exploit completion. |
| `check`                        | Check if the target is vulnerable.                        |
| `exploit`                      | Execute the exploit.                                      |
| `exploit -j`                   | Run the exploit as a background job.                      |
| `exploit -z`                   | Execute without interacting with the session.             |
| `exploit -e <encoder>`         | Use a specific payload encoder.                           |
| `sessions -l`                  | List active sessions.                                     |
| `sessions -l -v`               | List sessions with verbose details.                       |
| `sessions -s <script>`         | Run a script on all Meterpreter sessions.                 |
| `sessions -K`                  | Kill all sessions.                                        |
| `sessions -c <cmd>`            | Execute a command across all sessions.                    |
| `sessions -u <sessionID>`      | Upgrade a shell to Meterpreter.                           |
| `db_create <name>`             | Create a database for storing attack results.             |
| `db_connect <name>`            | Connect to a database.                                    |
| `db_nmap`                      | Run Nmap and save results in the database.                |
| `db_destroy`                   | Delete the active database.                               |

---

### **Meterpreter Commands**

|**Command**|**Description**|
|---|---|
|`help`|Display Meterpreter help.|
|`run <script>`|Execute a Meterpreter script.|
|`sysinfo`|Display system information of the target.|
|`ls`|List files/directories on the target.|
|`use priv`|Load privilege escalation extensions.|
|`ps`|Display all running processes.|
|`migrate <PID>`|Migrate to a specific process.|
|`use incognito`|Load token-stealing features.|
|`list_tokens -u`|List user tokens.|
|`list_tokens -g`|List group tokens.|
|`impersonate_token <token>`|Impersonate a specific token.|
|`steal_token <PID>`|Steal a process token.|
|`drop_token`|Stop token impersonation.|
|`getsystem`|Attempt to gain SYSTEM privileges.|
|`shell`|Open an interactive shell.|
|`execute -f <cmd.exe>`|Run a process (e.g., `cmd.exe`).|
|`rev2self`|Revert to the original user.|
|`reg <command>`|Interact with the target's registry.|
|`setdesktop <number>`|Switch desktop sessions.|
|`screenshot`|Capture a screenshot of the target.|
|`upload <file>`|Upload a file to the target.|
|`download <file>`|Download a file from the target.|
|`keyscan_start`|Start capturing keystrokes.|
|`keyscan_dump`|Dump captured keystrokes.|
|`keyscan_stop`|Stop keystroke logging.|
|`getprivs`|Get as many privileges as possible.|
|`uictl enable <keyboard/mouse>`|Control the target's keyboard/mouse.|
|`background`|Run the current session in the background.|
|`hashdump`|Dump all password hashes.|
|`use sniffer`|Load the packet sniffer module.|
|`sniffer_interfaces`|List available network interfaces.|
|`sniffer_start <ID>`|Start sniffing on an interface.|
|`sniffer_stop <ID>`|Stop packet sniffing.|
|`add_user <user> <pass>`|Create a user on the target.|
|`add_group_user <group> <user>`|Add a user to a specific group.|
|`clearev`|Clear event logs on the target.|
|`timestomp`|Modify file timestamps.|
|`reboot`|Reboot the target.|

---
