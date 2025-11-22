
https://github.com/s0md3v/XSStrike?tab=readme-ov-file

---

`XSStrike` is an advanced **XSS (Cross-Site Scripting) detection and exploitation tool** written in Python. It's often used by security researchers and penetration testers to test web applications for XSS vulnerabilities.

----
# Installation    
```sh
cd bin
git clone https://github.com/s0md3v/XSStrike
cd XSStrike
pip install -r requirements.txt --break-system-packages
```

# Make alias in `.bashrc` file
```sh
alias xsstrike='python3 /home/am/bin/XSStrike/xsstrike.py'
```

# Usage
```bash
xsstrike -u <target_url>
```

# Basic scan
```sh
xsstrike -u "http://example.com/search.php?q=test"
```

# Crawl the website and test each parameter:
```sh
xsstrike -u "http://example.com" --crawl
```

# Use a specific HTTP method (GET or POST)
```sh
xsstrike -u "http://example.com" --method POST
```

# Set custom headers (e.g., cookies, user-agent)
```sh
xsstrike -u "http://example.com" --headers "Cookie: session=abcd1234; User-Agent: Firefox"
```

# Fuzz specific parameter
```sh
xsstrike -u "http://example.com/index.php?name=admin" --fuzzer
```

# Use Tor for anonymity:
```sh
xsstrike -u "http://example.com" --tor
```


---
# Common Options

| Option      | Description                           |
| ----------- | ------------------------------------- |
| `-u`        | Target URL                            |
| `--crawl`   | Crawl the site and test found links   |
| `--params`  | List all parameters                   |
| `--fuzzer`  | Launch the intelligent payload fuzzer |
| `--update`  | Update XSStrike                       |
| `--timeout` | Set timeout (seconds)                 |
| `--tor`     | Route traffic through Tor             |
| `--headers` | Add custom headers                    |