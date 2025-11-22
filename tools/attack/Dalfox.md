
It’s a powerful, fast, and modern XSS scanner written in Go that supports **reflected**, **stored**, **blind**, and **DOM-based XSS** detection.

**Install Dalfox**
```bash
go install github.com/hahwul/dalfox/v2@latest
```

**To uninstall**
```bash
cd ~/go/bin
rm -rf dalfox
```

----

# Basic Usage 

## Scan a single URL
```bash
dalfox url "https://example.com/search?q=test"
```

## Use GET and POST methods
```bash
dalfox url "https://example.com/search?q=test" -X POST --data "q=test"
```

## Smart scanning with parameter mining
`Dalfox` can automatically find parameters in the page and scan them.
```bash
dalfox url "https://example.com/page" --deep-dive
```

## Use custom payloads
```bash
dalfox url "https://example.com?q=param" --custom-payload payloads.txt
```

## Blind XSS detection (with webhook)
```bash
dalfox url "https://example.com?q=hello" --blind "https://your-bxss-server.com"
```

## Scan from file
```bash
dalfox file urls.txt
```
Where `urls.txt` might contain:
```
https://example.com/page.php?input=1
https://testsite.com/search?q=hello
```

## Use cookies, headers, tokens
```bash
dalfox url "https://example.com" -H "Cookie: sessionid=abc123" -H "User-Agent: Dalfox"
```

##  Use --browser for Real DOM-Based XSS (Headless Execution)
Dalfox supports headless Chromium via Selenium to detect real DOM behavior:
```bash
dalfox url "https://example.com/page?search=test" --browser
```
- This launches **headless Chrome**, injects payloads, and **executes** the page to detect XSS via real DOM behavior.
- It can detect issues like:
    - Payloads reflected in `innerHTML`, `location`, `eval`, etc.
    - Triggers like JavaScript alerts or script execution.

## Step-by-Step: Using Dalfox for DOM-based XSS
```bash
dalfox url "https://example.com/page?query=hello" --deep-domxss
```
- Insert DOM-based XSS payloads.
- Detect **sinks** like `document.write`, `innerHTML`, etc., in the response.
- It does **not execute** the JavaScript; it only analyzes the code statically.
+ ==⚠️== This is **static analysis**, so it's limited for real DOM-XSS detection.
+ If you're serious about DOM-XSS hunting, you might also combine Dalfox with tools like:
	- **XSStrike** (DOM fuzzing)
	- **Burp Suite** with DOM Invader
	- **Manually analyzing JS with DevTools**

* * *

# Examples by Use Case

## Reflected XSS test:
```bash
dalfox url "https://example.com/search?q=dalfox"
```

## Stored XSS test (e.g., via POST to a comment field):
```bash
dalfox url "https://example.com/comment" -X POST --data "comment=dalfox"
```

## Param mining + header injection:
```bash
dalfox url "https://example.com" --deep-dive --only-poc
```

## Example for Real Use:
```bash
dalfox url "https://vulnerable.site/search?q=test" \
  --blind "https://your-interactsh.com" \
  -H "Cookie: sessionid=abc123" \
  --deep-dive --only-poc --output results.json
```
**Use proxy**
```bash
dalfox url "https://target.com" --proxy "http://127.0.0.1:8080"
```

---

# Useful Flags Summary

| Flag | Description |
| --- | --- |
| `--only-poc` | Show only proof-of-concept payloads |
| `--blind <url>` | Blind XSS testing |
| `--deep-dive` | Enable param mining + in-depth scanning |
| `--custom-payload` | Load your own payloads from file |
| `-H` | Custom headers (e.g., cookies, user-agent) |
| `-X` | HTTP method (e.g., POST) |
| `--data` | POST data |
| `--output` | Save results to a file (JSON supported) |