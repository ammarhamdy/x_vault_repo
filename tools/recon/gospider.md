
https://www.kali.org/tools/gospider/

----

This package contains a Fast web spider written in Go. 
The features are: 
- Fast web crawling 
- Brute force and parse `sitemap.xml` 
- Parse `robots.txt` 
- Generate and verify link from JavaScript files 
- Link Finder 
- Find `AWS-S3` from response source 
- Find subdomains from response source 
- Get URLs from `Wayback Machine`, Common Crawl, Virus Total, Alien Vault 
- Format output easy to Grep 
- Support Burp input 
- Crawl multiple sites in parallel 
- Random mobile/web `User-AgentShowcases`


```bash
go install github.com/jaeles-project/gospider@latest
```


---

# Examples

## Crawl a Single Target
```bash
gospider -s https://example.com
```
This will crawl the homepage and collect:
- Links (`href`, `src`)
- JavaScript files
- Parameters in query strings

## Depth Control
```bash
gospider -s https://example.com --depth 2
```

## Multi-threaded Crawling
```bash
gospider -s https://example.com -t 10
```

## Filter by Subdomain
```bash
gospider -s https://example.com --include-subs
```
- Also crawls subdomains found in links like `sub.example.com`.

## Read URLs from a File
```bash
gospider -S urls.txt -t 10 --depth 2 -o output/
```
Where `urls.txt` contains:
``` 
https://target1.com
https://target2.com
```

## Set User-Agent and Headers
```bash
gospider -s https://target.com \
  --user-agent "Mozilla/5.0" \
  --header "X-Api-Key: mykey123"
```

