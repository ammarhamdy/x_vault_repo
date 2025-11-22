`DMitry` (Deep-magic Information Gathering Tool)

https://www.kali.org/tools/dmitry/

---

**`DMitry`** is a small UNIX/Linux command-line information-gathering utility that consolidates a number of quick reconnaissance tasks (`whois`, `netcraft`, subdomain discovery, e-mail harvesting, basic TCP port-scan, banner grabbing, up-time info, etc.) into a single tool.

---
# Installation
```sh
sudo apt install dmitry
```

# Quick use
```sh
dmitry -winsepo example.txt example.com
```

|Option|Description|
|---|---|
|`-w`|Perform a standard WHOIS lookup on the host.|
|`-i`|Perform an Internet Number (IP) WHOIS lookup (RIPE/ARIN/etc.) on the IP.|
|`-n`|Fetch Netcraft data (OS, web server, uptime info where available).|
|`-s`|Perform a subdomain search (tries multiple engines to find subdomains).|
|`-e`|Search for e-mail addresses related to the target (similar technique to subdomain search).|
|`-p`|Perform a TCP port scan for the target (lists open/closed/filtered ports).|
|`-f`|With `-p`, show filtered ports too.|
|`-b`|With `-p`, request/print banners when available.|
|`-t`|Set the timeout (TTL) for port scanning (default is 2s; increase if the host is slow or behind a firewall).|
|`-o filename`|Write the output to `filename` (if omitted writes to STDOUT; if used without a name it uses `target.txt`). **`-o` must appear last.**|

