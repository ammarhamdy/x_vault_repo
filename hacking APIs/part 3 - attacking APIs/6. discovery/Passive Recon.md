

Passive reconnaissance is the act of obtaining information about a target
without directly interacting with the target’s devices. When you take this
approach, your goal is to find and document your target’s attack surface
without making the target aware of your investigation.

# `OSINT`

Typically, passive reconnaissance leverages **open-source intelligence** (`OSINT`), which is data collected from publicly available sources.

You will be on the hunt for API endpoints, credential information, version information, API documentation, and information about the API’s business purpose.


## Phase One: Cast a Wide Net
Search the internet for very general terms to learn some fundamental
information about your target.

Search engines such as **Google**, **`Shodan`**, and **`ProgrammableWeb`** can help you find general information about the API

Additionally, you need to investigate your target’s attack surface.
This can be done with tools such as `DNS` Dumpster and `OWASP` `Amass`.

## Phase Two: Adapt and Focus
Next, take your findings from phase one and adapt your `OSINT` efforts to
the information gathered.

This might mean increasing the specificity of your search queries.

## Phase Three: Document the Attack Surface
Taking notes is crucial to performing an effective attack. Document and
take screen captures of all interesting findings.

Create a task list of the passive reconnaissance findings that could prove useful throughout the rest of the attack.



# Google Hacking

Google hacking (also known as Google dorking) involves the clever use of advanced search parameters and can reveal all sorts of public API-related information about your target, including vulnerabilities, API keys, and usernames, that you can leverage during an engagement.
https://en.wikipedia.org/wiki/Google_hacking

In addition to your own carefully crafted Google search queries, you can use Offensive Security’s Google Hacking Database 
(`GHDB`, https://www.exploit-db.com/google-hacking-database). 
The `GHDB` ==is a repository of queries that reveal publicly exposed vulnerable systems and sensitive information.==

some useful API queries from the `GHDB`:
+ `inurl:"/wp-json/wp/v2/users"`
+ `intitle:"index.of" intext:"api.txt"`
+ `inurl:"/includes/api/" intext:"index of /"`
+ `ext:php inurl:"api.php?action="`
+ `intitle:"index of" api_key OR "api key" OR apiKey -pool`


# Programmable-Web’s API Search Directory

Other sites with API repositories include 
+ https://rapidapi.com 
+ and https://apis.guru/browse-apis.


# `Shodan`
`Shodan` is the go-to search engine for devices accessible from the internet.

`Shodan` regularly scans the entire `IPv4` address space for systems with open
ports and makes their collected information public at https://shodan.io. 

You can use `Shodan` to discover external-facing APIs and get information about
your target’s open ports, making it useful if you have only an IP address or organization’s name to work from.

Like with Google dorks, you can search `Shodan` casually by entering your target’s domain name or IP addresses; alternatively, you can use search parameters as you would when writing Google queries.

some useful Shodan queries:
+ `hostname:"targetname.com"`
+ `"content-type: application/json"`
+ `"content-type: application/xml"`
+ `"200 OK"`
	+ if an API does not accept the format of `Shodan`’s request, it will likely issue a 300 or 400 response.
+ `"wp-json"`
	+ This will search for web applications using the WordPress API.


# `OWASP` Amass

`OWASP` Amass is a command line tool that can map a target’s external network by collecting `OSINT` from over **55** different sources. 

You can set it to perform passive or active scans.

If you choose the active option, Amass will collect information directly from the target by requesting its certificate information. 

Otherwise, it collects data from search engines (such as `Google`, `Bing`, and `HackerOne`), `SSL` certificate sources (such as `GoogleCT`, `Censys`, and `FacebookCT`), search APIs (such as `Shodan`, `AlienVault`, `Cloudflare`, and GitHub), and the web archive Way-back.

```
amass enum -passive -d twitter.com |grep api
```

Use the intel command to collect `SSL` certificates, search reverse `Whois` records, and find `ASN` IDs associated with your target. 

Start by providing the command with target IP addresses:
```
amass intel -addr <target IP addresses>
```
If this scan is successful, it will provide you with domain names.

These domains can then be passed to intel with the `whois` option to perform a
reverse `Whois` lookup:
```
amass intel -d <target domain> –whois
```

The active enum scan will perform much of the same scan as the passive
one, but it will add domain name resolution, attempt `DNS` zone transfers,
and grab `SSL` certificate information:
```
amass enum -active -d <target domain>
```

To up your game, add the -brute option to brute-force subdomains, `-w` to specify the `API_superlist` `wordlist`, and then the `-dir` option to send the output to the directory of your choice:
```
amass enum -active -brute -w /usr/share/wordlists/API_superlist -d <target domain> -dir <directory name>
```

If you’d like to visualize relationships between the data Amass returns, use the `viz` sub-command:
```
amass viz -enum -d3 -dir <directory name>
```
Amass visualization using `-d3` to make an HTML export of Amass findings for the target.



# Exposed Information on GitHub

Searching GitHub for `OSINT` could reveal your target’s API capabilities, documentation, and secrets, such as admin-level API keys, passwords, and tokens,
which could be useful during an attack.

