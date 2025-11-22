
https://commixproject.com/

https://www.kali.org/tools/commix/

---

```bash
git clone https://github.com/commixproject/commix.git commix
```

**Create alias for commix in `.bashrc` file** 
```
alias commix='python3 /opt/commix/commix.py'
```

**Commix** — a powerful tool for exploiting **Command Injection** vulnerabilities.

**Commix** (short for **\[COM\]mand \[I\]njection e\[X\]ploiter**) is an open-source penetration testing tool written in Python. 

It's designed to **automate the detection and exploitation of command injection vulnerabilities** in web applications.

**Features**
- Detects and exploits **classic command injection** vulnerabilities.
- Supports **GET**, **POST**, **cookie**, and **header** parameters.
- Interactive shell after successful exploitation.
- Payload customization and bypass techniques.
- Works with various **WAF evasion** techniques.

---

# Basic Options Explained

`--url` --> The target URL with a vulnerable parameter.

`--data` --> Use this for POST requests (e.g., `param1=value1&param2=value2`).

`--cookie` --> Set cookies if the app requires login/session.

`--user-agent`, `--referer`, etc. -->  Useful for bypassing filters or emulating browsers.

---

# Advanced Features

`--level=3` and `--risk=3` --> Use these to test more parameters and deeper payloads.

`--os-shell` --> If vulnerable, drops you into an interactive shell.

`--batch` --> Run without asking for user input (non-interactive).

`--technique=“T”` --> Specify injection technique (`T` = time-based, `C` = classic, etc.).

`--tamper=...` --> Use tamper scripts to bypass filters.

---

# Example Usage Scenarios


```bash
commix --url="http://target.com/page.php?param=value"
```
This command tells Commix to test the `param` parameter for command injection vulnerabilities.

## Simple GET request test
```bash
commix --url="http://example.com/page.php?id=1"
```

## POST parameter test
```bash
commix --url="http://example.com/login.php" --data="username=admin&password=admin"
```

## With cookies (e.g., after login)
```bash
commix --url="http://example.com/dashboard.php?id=2" --cookie="PHPSESSID=abc123"
```

## Using authentication
```bash
commix --url="http://example.com/secret.php?id=1" --auth-type="basic" --auth-cred="user:pass"
```

## Advanced

```bash
commix --url="http://example.com/page.php?id=1" --os-shell --batch
```

```bash
commix --url="http://192.168.0.23/commix-testbed/scenarios/user-agent/ua(eval).php" --level 3
```