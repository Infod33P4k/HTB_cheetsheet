# Nmap Options Cheat Sheet

## Scanning Options
| **Nmap Option**               | **Description**                                                               |
|-------------------------------|-------------------------------------------------------------------------------|
| `10.10.10.0/24`               | Target network range.                                                        |
| `-sn`                         | Disables port scanning.                                                      |
| `-Pn`                         | Disables ICMP Echo Requests.                                                 |
| `-n`                          | Disables DNS Resolution.                                                     |
| `-PE`                         | Performs the ping scan using ICMP Echo Requests.                             |
| `--packet-trace`              | Shows all packets sent and received.                                         |
| `--reason`                    | Displays the reason for a specific result.                                   |
| `--disable-arp-ping`          | Disables ARP Ping Requests.                                                  |
| `--top-ports=<num>`           | Scans the top ports defined as most frequent.                                |
| `-p-`                         | Scan all ports.                                                              |
| `-p22-110`                    | Scan all ports between 22 and 110.                                           |
| `-p22,25`                     | Scans only the specified ports 22 and 25.                                    |
| `-F`                          | Scans top 100 ports.                                                         |
| `-sS`                         | Performs a TCP SYN-Scan.                                                     |
| `-sA`                         | Performs a TCP ACK-Scan.                                                     |
| `-sU`                         | Performs a UDP Scan.                                                         |
| `-sV`                         | Scans discovered services for their versions.                                |
| `-sC`                         | Performs a Script Scan with default scripts.                                 |
| `--script <script>`           | Performs a Script Scan using specified scripts.                              |
| `-O`                          | Performs an OS Detection Scan to determine the OS of the target.             |
| `-A`                          | Performs OS Detection, Service Detection, and traceroute scans.              |
| `-D RND:5`                    | Sets the number of random Decoys used to scan the target.                    |
| `-e`                          | Specifies the network interface used for the scan.                           |
| `-S 10.10.10.200`             | Specifies the source IP address for the scan.                                |
| `-g`                          | Specifies the source port for the scan.                                      |
| `--dns-server <ns>`           | Performs DNS resolution using a specified name server.                       |

---

## Output Options
| **Nmap Option**               | **Description**                                                               |
|-------------------------------|-------------------------------------------------------------------------------|
| `-oA filename`                | Stores results in all formats starting with the name "filename".             |
| `-oN filename`                | Stores results in normal format with the name "filename".                    |
| `-oG filename`                | Stores results in "grepable" format with the name "filename".                |
| `-oX filename`                | Stores results in XML format with the name "filename".                       |

---

## Performance Options
| **Nmap Option**               | **Description**                                                               |
|-------------------------------|-------------------------------------------------------------------------------|
| `--max-retries <num>`         | Sets the number of retries for scans of specific ports.                      |
| `--stats-every=5s`            | Displays scan's status every 5 seconds.                                      |
| `-v` / `-vv`                  | Displays verbose output during the scan.                                     |
| `--initial-rtt-timeout 50ms`  | Sets the specified time value as initial RTT timeout.                        |
| `--max-rtt-timeout 100ms`     | Sets the specified time value as maximum RTT timeout.                        |
| `--min-rate 300`              | Sets the number of packets sent simultaneously.                              |
| `-T <0-5>`                    | Specifies a timing template. (0 = paranoid, 5 = insane)                      |
