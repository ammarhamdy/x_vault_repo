
https://github.com/sullo/nikto/wiki
https://www.kali.org/tools/nikto/

---

`Nikto` is an open-source web server scanner designed to identify vulnerabilities and misconfigurations in web servers. 

It’s easy to use and great for quick reconnaissance.

`Nikto` is **==loud==** — ==it’s not stealthy and can be easily detected==.

```bash
sudo apt install nikto
```

---

# Basic Usage

**Scan a Website**
```bash
nikto -h http://example.com
```

---

# Common Options

| Option                | Description                                                                      |
| --------------------- | -------------------------------------------------------------------------------- |
| `-h <host>`           | Target hostname or IP                                                            |
| `-p <port>`           | Target port (default 80 or 443)                                                  |
| `-ssl`                | Force SSL connection                                                             |
| `-Tuning <options>`   | Choose types of tests (e.g., 1 for interesting files, 9 for SQL injection, etc.) |
| `-output <file>`      | Save output to a file (e.g., `.txt`, `.html`)                                    |
| `-Format <type>`      | Output format: `csv`, `html`, `xml`, `json`                                      |
| `-Useragent <string>` | Custom user agent                                                                |

---

# Example Command

## Scan an IP Directly
```bash
nikto -h http://192.168.1.100
```

## Scan Multiple Hosts from a File
```bash
nikto -h targets.txt
```

## Scan a Specific Port
```bash
nikto -h http://example.com -p 8080
```

## Want to scan a specific directory or virtual host?
```bash
nikto -h http://example.com/admin/
```

```bash
nikto -h http://192.168.1.100 -vhost dev.example.com
```

## Perform Specific Test Types (Tuning)
```bash
nikto -h http://example.com -Tuning x
```
`x` can be a digit or letter. 
Examples:

|Code|Test Type|
|---|---|
|1|Interesting files / dirs|
|2|Misconfigurations|
|3|Default files|
|4|Injection vulnerabilities|
|5|Remote file inclusion|
|9|SQL injection|
|b|Authentication bypass|

## Test for `SQLi` and misconfig
```bash
nikto -h http://example.com -Tuning 29
```

## Output Results to File (TXT/HTML/XML/JSON)

```bash
nikto -h http://example.com -output scan.txt
```

```bash
nikto -h http://example.com -output scan.html -Format html
```

## Set a Custom User-Agent
```bash
nikto -h http://example.com -useragent "Mozilla/5.0 NiktoTest"
```

## Use a Proxy
```bash
nikto -h http://example.com -useproxy http://127.0.0.1:8080
```

## Throttle Request Speed
```bash
nikto -h http://example.com -delay 2
```
Adds a 2-second delay between requests to avoid overwhelming the server.

## Skip SSL Certificate Checks
```bash
nikto -h https://example.com -nossl
```

