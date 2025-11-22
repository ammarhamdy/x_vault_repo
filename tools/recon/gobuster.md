
`gobuster` is a super-handy tool for fast forced-discovery on web targets. 

 **What is `Gobuster`?**
**`Gobuster`** is a fast, command-line enumeration tool written in Go.  

It’s mainly used to discover:
- hidden directories and files on web servers (`dir` mode),
- DNS subdomains (`dns` mode),
- virtual hosts / vhosts (`vhost` mode),
- and more (plugins/variants exist).

It works by making many concurrent HTTP/DNS requests using entries from a wordlist.

---
# Available Commands (modes)

`completion` 
Generate the auto-completion script for the specified shell

`dir` Uses directory/file enumeration mode

`dns` Uses DNS subdomain enumeration mode

`fuzz`
Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body

`gcs` Uses gcs bucket enumeration mode

`help` Help about any command

`s3` Uses aws bucket enumeration mode

`tftp` Uses `TFTP` enumeration mode

`version` shows the current version

`vhost`
Uses `VHOST` enumeration mode (you most probably want to use the IP address as the URL parameter)

---

# Performance & tuning tips

- **Threads:** increase `-t` to use more concurrency on capable networks/targets (start conservative: 10–50, then ramp).
    
- **Use targeted wordlists:** big generic lists are slower; use focused lists (`SVNDigger`, `SecLists`, language/framework-specific lists).
    
- **Filter responses:** set `-s` to only show useful status codes to reduce noise.
    
- **Wildcard detection:** enable `--wildcard` if the server returns 200 for unknown paths (helps avoid false positives).
    
- **Proxying & debugging:** route through Burp (`-p http://127.0.0.1:8080`) for inspection, or use `-o` to save results and review later.
    
- **Rate-limit:** be polite—use delays or lower thread counts against production targets. Rapid aggressive scans can bring down services or trigger WAFs.
    
- **Parallelize smartly:** if you have many wordlists, split them into chunks and run multiple `gobuster` jobs distributed over time/threads.

---
# `dir`  mode

`-a, --useragent string ` 
Set the User-Agent string (default "`gobuster/3.6`")

`-t, --threads int `
Number of concurrent threads (default 10)

`-s, --status-codes string`
Positive status codes (will be overwritten with status-codes-blacklist if set). Can also handle ranges like 200,300-400,404.

`-o, --output string`
Output file to write results to (defaults to stdout)

`-x, --extensions string`
File extension(s) to search for

`-d, --discover-backup`
Also search for backup files by appending multiple backup extensions

`--timeout duration`
HTTP Timeout (default 10s)

```sh
gobuster dir -u https://example.com \
  -w /path/to/wordlists/common.txt \
  -t 50 \
  -x php,html,js,txt \
  -s 200,204,301,302,401,403 \
  -o gobuster_dir.txt \
  --wildcard
```

```sh
gobuster dns -d example.com \
  -w /path/to/wordlists/subdomains.txt \
  -t 50 \
  -o gobuster_dns.txt \
  -p http://127.0.0.1:8080 # optional: route through Burp
```

```sh
gobuster dir -u https://example.com -w /wl.txt -t 40 \
  -a "MyAgent/1.0" -k \
  --timeout 10 -o out.txt
```

----