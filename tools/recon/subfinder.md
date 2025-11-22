
https://www.kali.org/tools/subfinder/

[https://github.com/projectdiscovery/subfinder/releases](https://github.com/projectdiscovery/subfinder/releases)

`subfinder` is a popular subdomain enumeration tool developed by `ProjectDiscovery`.

---
# Install via Go

**Install Go**
```bash
sudo apt install golang-go -y
```

**Install `subfinder`**
```bash
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

**Create alias on `.bashrc` file**
```
alias subfinder='/home/am/go/bin/subfinder'
```

---

# Configuration (Recommended)

Create the config file and set up your API keys for better results:
```bash
subfinder -config ~/.config/subfinder/config.yaml
```
You can get free API keys from:
* `SecurityTrails`
* `VirusTotal`
* `Shodan`
* `Censys`
* `Spyse`
* And more (full list in their docs)

---

# Basic Usage

## Find subdomains of a target
```bash
subfinder -d example.com
```

## Save results to a file
```bash
subfinder -d example.com -o subdomains.txt
```

## Use silent mode (no banners or logs)
```bash
subfinder -d example.com -silent
```

## Use multiple domains from a file:
```bash
subfinder -dL domains.txt -o results.txt
```

---

# Configuration 


By default, `subfinder` looks for a config file at:
```
~/.config/subfinder/config.yaml
```
If it doesn't exist, you can create it manually:


## Structure of `config.yaml`
```yaml
resolvers:
  - 1.1.1.1
  - 8.8.8.8

sources:
  - alienvault
  - anubis
  - bufferover
  - censys
  - certspotter
  - chaos
  - crtsh
  - dnsdb
  - github
  - intelx
  - passivetotal
  - robtex
  - securitytrails
  - shodan
  - spyse
  - virustotal

binary: ""

censys:
  id: YOUR-CENSYS-ID
  secret: YOUR-CENSYS-SECRET

github:
  - YOUR-GITHUB-TOKEN

securitytrails:
  apikey: YOUR-SECURITYTRAILS-APIKEY

shodan:
  apikey: YOUR-SHODAN-APIKEY

spyse:
  apikey: YOUR-SPYSE-APIKEY

virustotal:
  apikey: YOUR-VIRUSTOTAL-APIKEY

intelx:
  apikey: YOUR-INTELX-APIKEY
  eid: YOUR-EID (optional)

passivetotal:
  username: YOUR-PASSIVETOTAL-USERNAME
  apikey: YOUR-PASSIVETOTAL-APIKEY
```


## Where to Get API Keys
Here’s where to sign up:

| Source             | URL                                                                      |
| ------------------ | ------------------------------------------------------------------------ |
| **VirusTotal**     | https://www.virustotal.com/gui/join-us                                   |
| **Shodan**         | https://account.shodan.io/register                                       |
| **SecurityTrails** | https://securitytrails.com/app/account                                   |
| **Censys**         | https://search.censys.io/account/api                                     |
| **GitHub Token**   | [https://github.com/settings/tokens](https://github.com/settings/tokens) |
| **IntelX**         | https://intelx.io/signup                                                 |
| **PassiveTotal**   | https://community.riskiq.com/register                                    |
