
# Performing [Reconnaissance](https://translate.google.com/?sl=en&tl=ar&text=Reconnaissance&op=translate) with OWASP Amass

https://github.com/owasp-amass/amass/blob/master/doc/tutorial.md

OWASP Amass is an open-source information-gathering tool that can be used for passive and active reconnaissance.

We will be using Amass to discover the attack surface of our target organizations. 

With as little as a target’s domain name, you can use Amass to scan through many internet sources for your target’s associated domains and subdomains to get a list of potential target URLs and APIs.



# Discovering API Endpoints with Kiterunner

is a content discovery tool designed specifically for finding API resources. 

Kiterunner is built with Go, and while it can scan at a speed of 30,000 requests per second, it takes into account the fact that load balancers and web application ==**firewalls will likely enforce rate limiting**==.

When it comes to APIs, Kiterunner’s search techniques outperform
other content discovery tools such as `dirbuster`, `dirb`, `Gobuster`, and `dirsearch` because this tool was built with API awareness.

Its wordlists, request methods, parameters, headers, and path structures are all focused on finding API endpoints and resources. Of note, the tool includes data from 67,500 Swagger files.

Kiterunner has also been designed to detect the signature of different APIs, including `Django`, `Express`, `FastAPI`, `Flask`, `Nginx`, `Spring`, and Tomcat (just to name a few).

**==All of the wordlists are hosted at==**:
	https://wordlists.assetnote.io/

download all the Assetnote wordlists at once:
```
wget -r --no-parent -R "index.html*" https://wordlists-cdn.assetnote.io/data/ -nH
```



# Scanning for Vulnerabilities with `Nikto`

`Nikto` is a command line web application vulnerability scanner that is quite effective at information gathering.

As it can point me toward the application’s interesting aspects.

To scan a domain, use the following command:
```
Nikto -h https://example.com
```

To see the additional `Nikto` options, enter `Nikto` `-Help` on the command line. 

A few options you may find useful include -output filename for saving the `Nikto` results to a specified file and `-maxtime` `#ofseconds` to limit how long a `Nikto` scan will take.

see:
https://github.com/sullo/nikto/wiki


# Scanning for Vulnerabilities with OWASP ZAP

OWASP developed ZAP, an open-source web application scanner, and it’s another essential web application security testing tool.

OWASP ZAP should be included in Kali, but if it isn’t, you can clone it from GitHub at:
	https://github.com/zaproxy/zaproxy.



# Fuzzing with `Wfuzz`

`Wfuzz` is an open-source Python-based web application fuzzing framework. 

`Wfuzz` should come with the latest version of Kali, but you can install it from GitHub at:
	https://github.com/xmendez/Wfuzz.

You can use `Wfuzz` to inject a payload within an HTTP request by
replacing occurrences of the word FUZZ with words from a wordlist; `Wfuzz` will then rapidly perform many requests (around 900 requests per minute) with the specified payload. 

==Since so much of the success of fuzzing depends on the use of a good wordlist==.

```
wfuzz options -z payload,params url
```

```
wfuzz -z file,/usr/share/wordlists/list.txt http://targetname.com/FUZZ
```
This command replaces FUZZ in the URL `http://targetname.com/FUZZ` with words from `/usr/share/wordlists/list.txt`. 
The `-z` option specifies a type of payload followed by the actual payload.

You can use the range option to easily scan a series of numbers:
```
wfuzz -z range,500-1000 http://targetname.com/account?user_id=FUZZ
```

To specify multiple attack positions, you can list off several `-z` flags and then number the corresponding `FUZZ` placeholders, such as `FUZZ`, `FUZ1`, `FUZ2`, `FUZ3`, and so on, like so:
```
wfuzz -z list,A-B-C -z range,1-3 http://targetname.com/FUZZ/user_id=FUZZ2
```

you should familiarize yourself with the `Wfuzz` filter options. 
The following filters display only certain results:
`--sc`  Only shows responses with specific HTTP response **==codes==**
`--sl`  Only shows responses with a certain number of **==lines==**
`--sw`  Only shows responses with a certain number of **==words==**
`--sh`  Only shows responses with a certain number of **==characters==**

In the following example, `Wfuzz` will scan the target and only show
results that include a status code of `200`:
```
wfuzz -z file,/usr/share/wordlists/list.txt -–sc 200 http://targetname.com/FUZZ
```

The following filters hide certain results:
`--hc`  Hides responses with specific HTTP status **==codes==**
`--hl`  Hides responses with a specified number of **==lines==**
`--hw`  Hides responses with a specified number of **==words==**
`--hh`  Hides responses with specified number of **==characters==**

In the following example, `Wfuzz` will scan the target and hide all results that have a status code of `404` and hide results that have 950 characters:
```
wfuzz -z file,/usr/share/wordlists/list.txt -–sc 404 -–sh 950 http://targetname.com/FUZZ
```

`Wfuzz` is a powerful multipurpose fuzzing tool you can use to thoroughly test endpoints and find their weaknesses. 

For more information about `Wfuzz`, check out the documentation at:
	https://wfuzz.readthedocs.io/en/latest.



# Discovering HTTP Parameters with Arjun

`Arjun` is another open source **==Python-based==** API fuzzer developed specifically to discover web application parameters.

**==You can use it as a great first scan for an API endpoint during black box testing or as an easy way to see how well an API’s documented parameters match up with the scan’s findings==**

Arjun comes configured with a wordlist containing nearly **26,000**
parameters, and unlike `Wfuzz`, it does some of the filtering for you using its pre-configured anomaly detection.

To run Arjun, use the following command:
```
python3 /opt/Arjun/arjun.py -u http://target_address.com
```

