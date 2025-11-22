
https://www.kali.org/tools/nuclei/

https://www.youtube.com/watch?v=b5qMyQvL1ZA&list=PLZRbR9aMzTTpItEdeNSulo8bYsvil80Rl

----

Nuclei is one of the most impressive open source vulnerability scanners
released in recent years. Its advantage over other tools stems from its
 community-powered templating system, which reduces false positives by matching known patterns against responses it receives from network services and files.

Nuclei naturally supports common network services, such as HTTP,
DNS, and network sockets, as well as local file scanning. 

You can use it to send HTTP requests, DNS queries, and raw bytes over the network. 

Nuclei can even scan files to find credentials

---
# Nuclei templates

Nuclei has more than 8,000 templates in its database.

To get a list of all available templates run:
```sh
nuclei -tl
```
All templates are there: `~/nuclei-templates`  

Nuclei templates are based on YAML files with the following high-level
structure:

+ **`ID`** A unique identifier for the template

+ **`Metadata`** ​Information about the template, such as a description, the author, the severity, and tags (arbitrary labels that can group multiple templates, such as injection or denial of service)

 + **`Protocol`** The mechanism that the template uses to make its requests; for example, `http` is a protocol type that uses HTTP for web requests.

+ **`Operators`** Used for matching patterns against responses received by a template execution (`matchers`) and extracting data (extractors), similarly to the filtering performed by tools like grep

Here is a simple example of a Nuclei template that uses HTTP to find the default Apache HTML welcome page.
```yml
id: detect-apache-welcome-page

info:
	name: Apache2 Ubuntu Default Page
	author: Dolev Farhi and Nick Aleks
	severity: info
	tags: apache

http:
	- method: GET
		path:
			- '{{BaseURL}}'
	matchers:
			- type: word
			words:
				- "Apache2 Ubuntu Default Page: It works"
			part: body
```

As a result, when Nuclei performs a scan against an IP address that runs some form of a web server, this template will make a GET request to its base URL (/) and look for the string "`Apache2 ubuntu Default Page`"

If it finds this string in the response’s `body`, the check will be considered successful because the pattern matched.

Nuclei’s templating structure: https://docs.projectdiscovery.io/templates/structure

---
# Installation 
```sh
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

#  Basic Usage
```sh
nuclei -u https://example.com
```

# Scanning with Templates

Run a specific template:
```sh
nuclei -u https://example.com -t cves/2021/CVE-2021-1234.yaml
```

Run all templates from a directory:
```sh
nuclei -u https://example.com -t cves/
```

Run with multiple targets:
```sh
nuclei -l urls.txt -t exposures/
```

# Updating Templates

```sh
nuclei -update-templates
```
 
```sh
nuclei -ut
```

# Writing a Custom Template

Let’s write a simple template that finds the Git repositories

We’ll define multiple `BaseURL` paths to represent the two paths we’ve identified. 

Then, using Nuclei’s `matchers`, we’ll define a string `ref: refs/heads/master` to match the response body returned by the scanned server:
```yml
id: detect-git-repository

info:
 name: Git Repository Finder
 author: Dolev Farhi and Nick Aleks
 severity: info
 tags: git

http:
 - method: GET
 path:
  - '{{BaseURL}}/backup/acme-hyper-branding/.git/HEAD'
  - '{{BaseURL}}/backup/acme-impact-alliance/.git/HEAD'

matchers:
 - type: word

words:
 - "ref: refs/heads/master"

part: body
```

## Download template
Download this custom Nuclei template from the book’s GitHub repository at: https://github.com/projectdiscovery/nuclei-templates

# Running a Full Scan

When not provided with a specific template, Nuclei will use its built-in templates during the scan. 

Running Nuclei is noisy, so we recommend tailoring الخياطة the execution to a specific target.

For instance, if you know a server is running Apache, you could select just the Apache-related templates by specifying the `-tags` option:
```sh
nuclei -tags apache,git -u 172.16.10.11
```

