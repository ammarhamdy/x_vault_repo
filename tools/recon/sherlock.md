
https://www.kali.org/tools/sherlock/
---

`sherlock` designed for username reconnaissance across social media platforms and websites.

Takes a username as input and searches for that username across hundreds of social media sites and online platforms

**Key Features:**
- Searches across 400+ websites and social platforms
- Fast, automated checking using HTTP requests
- Can output results in multiple formats (JSON, CSV, etc.)
- Supports proxy usage for anonymity
- Color-coded terminal output showing found/not found results

**Common Use Cases:**
- Digital forensics investigations
- Background checks and due diligence
- Cybersecurity assessments
- Social engineering research (ethical contexts)
- Personal privacy audits

---
# Instillation
https://sherlockproject.xyz/installation#pypi-pip
```sh
pipx install sherlock-project
```

# Simple username search
```bash
sherlock john_doe
```

# Search multiple usernames
```sh
sherlock user1 user2 user3
```

# Save results to file
```sh
sherlock username --output results.txt
sherlock username --csv results.csv
sherlock username --json results.json
```

# Use proxy for anonymity
```sh
sherlock username --proxy http://127.0.0.1:8080
sherlock username --tor  # Use Tor proxy
```

# Search specific sites only
```sh
sherlock username --site GitHub --site Twitter
```

# Exclude certain sites
```sh
sherlock username --exclude Instagram --exclude Facebook
```

# Print only found results
```sh
sherlock username --print-found
```

# Timeout control
```sh
sherlock username --timeout 30  # 30 second timeout per site
```
