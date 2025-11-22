
https://www.kali.org/tools/ncrack/

---

`ncrack` is a powerful **network authentication cracking tool**, designed to perform **brute-force login attacks** on network services like SSH, RDP, FTP, Telnet, HTTP(S), VNC, SMB, and more. 

It's developed by the same team behind `nmap`.

`ncrack` is **not stealthy** by default. It's loud and will likely be logged.

**Install Ncrack**
```bash
sudo apt install ncrack
```

**Basic Syntax**
```bash
ncrack -p <port> <target>
```
**Or for a specific service:**
```bash
ncrack <service>://<target>
```

---

# Brute-force SSH login
```bash
ncrack -p 22 -U users.txt -P passwords.txt 192.168.1.100
```
- `-p 22`: target port
- `-U users.txt`: list of usernames
- `-P passwords.txt`: list of passwords
- `192.168.1.100`: target IP


# HTTP Login
```bash
ncrack -p http -U users.txt -P passwords.txt 192.168.1.100
```
Many HTTP-based logins today use forms or token-based systems—these may not be easily brute-forced via `ncrack`. 
For those, consider `hydra`.


# RDP (Windows Remote Desktop Protocol)
```bash
ncrack -p rdp -U users.txt -P passwords.txt 192.168.1.100
```


# FTP Login
```bash
ncrack -p ftp -U users.txt -P passwords.txt 192.168.1.100
```

|Option|Description|
|---|---|
|`-U`|Username list file|
|`-P`|Password list file|
|`-u`|Single username|
|`-p`|Port or service|
|`--user`|Inline user|
|`--pass`|Inline password|
|`-g`|Set timing (1–5, higher is faster but noisier)|
|`-vv`|Verbose output|


# **Supported Services**
Common ones include:
- `ssh`
- `ftp`
- `rdp`
- `telnet`
- `http`
- `vnc`
- `smtp`
- `pop3`
- `mysql`
- `postgres`

# Tips
- Start with low-intensity (`-T1`) to avoid lockouts.
- Combine with Nmap to find open ports:
```bash
nmap -p 21,22,3389 192.168.1.0/24 --open
```