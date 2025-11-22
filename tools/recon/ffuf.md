
https://www.kali.org/tools/ffuf/
---

`ffuf` (Fuzz Faster U Fool) is a fast web fuzzer written in Go, mainly used by penetration testers for directory brute-forcing, parameter fuzzing, virtual host discovery, and content discovery.

It’s like `dirbuster` or `gobuster`, but faster and with more options.

---
# Installation
```sh
sudo apt install ffuf
```

# Basic Usage
```sh
ffuf -c -w files_wordlist.txt -u http://172​.16​.10​.10:8081​/files/FUZZ
```
`FUZZ` → placeholder that `ffuf` replaces with words from the wordlist
`-c (color)` → highlight the results in the terminal.
`-w (wordlist)` → wordlist (to specify a custom wordlist).
`-u (URL)` → target URL

# Subdomain discovery
```sh
ffuf -u http://FUZZ.example.com -w subdomains.txt -H "Host: FUZZ.example.com"
```

# Parameter fuzzing
```sh
ffuf -u "http://example.com/index.php?FUZZ=test" -w params.txt
```

# Filtering results
You can filter by:
+ Response size (`-fs`)
+ Words count (`-fw`)
+ Status code (`-fc`):
```sh
ffuf -u http://example.com/FUZZ -w wordlist.txt -fc 404
```



