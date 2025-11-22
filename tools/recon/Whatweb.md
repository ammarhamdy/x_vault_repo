

The `WhatWeb` tool is a web scanner used to identify technologies used by websites. 

It can detect content management systems (CMS), web servers, programming languages, analytics tools, and much more.

```bash
sudo apt install whatweb
```

# Basic Usage

```
whatweb tatriz.codlop.sa
```

# Example Scans

**Scan with higher aggression level (deeper scan):**
```bash
./whatweb -a 3 https://example.com
```

**Scan multiple websites from a file:**
```bash
./whatweb -i targets.txt
```

**Use a proxy:**
```bash
./whatweb --proxy http://127.0.0.1:8080 https://example.com
```

**Save results to a file:**
```bash
./whatweb -v --log-verbose=scan_results.txt https://example.com
```

# **Useful Options**

| Option                     | Description                                     |
| -------------------------- | ----------------------------------------------- |
| `-v`                       | Verbose output (show plugin results)            |
| `--color=always`           | Force color output                              |
| `-a 3`                     | Aggression level (0-3, higher = more intrusive) |
| `--log-verbose=result.txt` | Save detailed results to a file                 |
| `-i input.txt`             | Scan multiple targets listed in a file          |
| `--proxy http://host:port` | Use an HTTP proxy                               |
| `--user-agent "UA"`        | Set a custom user-agent string                  |
| `--no-errors`              | Suppress errors in output                       |


---
# WhatWeb Plugins

`WhatWeb` uses **plugins** to identify technologies used by websites. 

These plugins are the core of WhatWeb’s detection capability—they define how to fingerprint different web technologies like CMS platforms, frameworks, web servers, analytics tools, and more.


## What Are WhatWeb Plugins?

- Plugins are written in **Ruby** and define **search patterns** or **rules** to detect specific technologies.
- Located in the `plugins/` directory (if installed via GitHub clone).
- Each plugin is a separate `.rb` file (e.g., `wordpress.rb`, `apache.rb`, `google-analytics.rb`).
- They check **headers**, **HTML content**, **cookies**, **meta tags**, etc.

**List all available plugins:**
```bash
whatweb --list-plugins
```

**Use a specific plugin only:**
```bash
whatweb --plugins=wordpress https://example.com
```
    
**Exclude a plugin:**
```bash
whatweb --no-plugins=google-analytics https://example.com
```

 **Enable debug mode to see plugin activity:**
```bash
whatweb -v --debug https://example.com
```
