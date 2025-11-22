
### Some Common Standard TCP Ports

| **Port** | **Protocol/Service** | **Description**                             |
| -------- | -------------------- | ------------------------------------------- |
| 20       | FTP (Data)           | File Transfer Protocol (data channel)       |
| 21       | FTP (Control)        | File Transfer Protocol (control channel)    |
| 22       | SSH                  | Secure Shell                                |
| 23       | Telnet               | Remote login service (insecure)             |
| 25       | SMTP                 | Simple Mail Transfer Protocol               |
| 53       | DNS                  | Domain Name System (TCP for zone transfers) |
| 80       | HTTP                 | HyperText Transfer Protocol (web traffic)   |
| 110      | POP3                 | Post Office Protocol v3 (email)             |
| 143      | IMAP                 | Internet Message Access Protocol            |
| 443      | HTTPS                | HTTP Secure (SSL/TLS encrypted)             |
| 3306     | MySQL                | MySQL database server                       |
| 5432     | PostgreSQL           | PostgreSQL database server                  |
| 3389     | RDP                  | Remote Desktop Protocol                     |


### Port Number Ranges

|**Range**|**Port Numbers**|**Usage**|
|---|---|---|
|Well-known|0–1023|Standard system ports for common services|
|Registered|1024–49151|Used by vendors for proprietary services|
|Dynamic/Private|49152–65535|Used by clients for temporary connections|